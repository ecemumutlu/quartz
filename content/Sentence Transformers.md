 - Sentence Transformers user guide blogpost ->  https://huggingface.co/blog/train-sentence-transformers#loss-function

 - SBert Blogpost -> https://towardsdatascience.com/sbert-deb3d4aef8a4

 - SBert documentation -> https://sbert.net/
 
 - SBert paper -> [[15-sbert.pdf]]
 
## [[Bi-encoders vs. Cross-encoders]]

# Blogpost keypoints

Steps: https://huggingface.co/blog/train-sentence-transformers#trainer
1. Load a model to finetune with
2. Load dataset 
3. Choose an appropriate loss function regarding the dataset from https://sbert.net/docs/sentence_transformer/loss_overview.html
4. Specify parameters using SentenceTransformersTrainingArguments https://sbert.net/docs/sentence_transformer/training_overview.html#training-arguments
5. (Optional) choose an evaluator and evaluate the base model according to the dev set
6. Create a trainer and train
7. (Optional) Evaluate the trained model on the test set, after training completes	
8. Save the trained model

transformer.TrainerCallback kullanarak training metric lerini bastırabilrisin.

### Multi-dataset training
Top-performing models are often trained using multiple datasets simultaneously. 
The [`SentenceTransformerTrainer`](https://sbert.net/docs/package_reference/sentence_transformer/SentenceTransformer.html#sentence_transformers.SentenceTransformer) simplifies this process by allowing you to train with multiple datasets without converting them to the same format. 
You can even apply different loss functions to each dataset.
Each training/evaluation batch will contain samples from only one of the datasets.



## Knowledge Check
[[11-hackerllama - Sentence Embeddings. Introduction to Sentence Embeddings.pdf]]

### Steps to use a Sentence Transformer
1. Install library
2. Load an existing sentence transformer model
3. Use encode method of the model to get the embeddings of the sentences
4. Check for similar sentences using cosine similarity -> instead: sentence transformers has semantic_search method that return the top-k most similar embeddings and their similariy score


**Word embeddings**  -> Glove, Word2Vec
**BERT Tokenizers**

 - BERT'te [CLS] tokeni tüm cümleye ait vektör embedding bilgisini taşıyor. Ama anlamı ortaya çıkartmak için bu vektörü linear layer + tanh activation function dan geçirmek gerekiyor. (Bu yapıda kullanırsak cls token representation'ı daha iyi öğreniyor)
	 - Bunu direkt modelin "pooler_output" undan retrieve edebiliriz
	 - model.pooler(model_output["last_hidden_state"])[0][:10]
	 - model_output["pooler_output"][0][:10]
 - Buna rağmen BERT kullanarak edineceğimiz vektör embedding BERT'in taskları için özel geliştirildiği için next word prediction taskı odaklı bir vektör. Sentence meaningi istediğimiz gibi elde edemiyoruz.
 - Bunun için kendi sentence transformer modelimizi eğitmemiz gerekiyor.


==the BERT [CLS] token is not trained to be a good sentence embedding. It’s trained to be a good sentence embedding for next-sentence prediction!==

Using a sentence transformer:
1. We tokenize the input sentence.
2. We process the tokens through the model.
3. We calculate the mean of the token embeddings.
4. We normalize the embeddings to ensure the embedding vector has a unit length.

```
import torch.nn.functional as F
from transformers import AutoModel, AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("sentence-transformers/all-MiniLM-L6-v2"
model = AutoModel.from_pretrained("sentence-transformers/all-MiniLM-L6-v2")



def mean_pooling(model_output):
	return torch.mean(model_output["last_hidden_state"], dim=1)
def get_sentence_embedding(text):
	encoded_input = tokenizer(text, return_tensors="pt")
	with torch.no_grad():
		model_output = model(**encoded_input)
		
	sentence_embeddings = mean_pooling(model_output)
	return F.normalize(sentence_embeddings)
	
get_sentence_embedding("Today is a sunny day")[0][:5]
```


In practice, you’ll likely be encoding batches of sentences, so we need to make some changes
• Modify the tokenization so we apply truncation (cutting the sentence if it’s longer than the
maximum length) and padding (adding [PAD] tokens to the end of the sentence).
• Modify the pooling so we take the attention mask into account. The attention mask is a vector of 0s and 1s that indicates which tokens are real and which are padding. We want to ignore the padding tokens when computing the mean!

 ```
def mean_pooling(model_output, attention_mask):
	token_embeddings = model_output["last_hidden_state"]
	input_mask_expanded = (
	attention_mask.unsqueeze(-1).expand(token_embeddings.size()).float())
	return torch.sum(token_embeddings, 1) / torch.clamp(input_mask_expanded.sum(1), min=1e-9)
	
# This now receives a list of sentences
def get_sentence_embedding(sentences):
	encoded_input = 
	  tokenizer(sentences, padding=True, truncation=True, return_tensors="pt")
	
	with torch.no_grad():
		model_output = model(**encoded_input)
		
	sentence_embeddings=mean_pooling(model_output,encoded_input["attention_mask"
	
	return F.normalize(sentence_embeddings)

query_embedding = get_sentence_embedding("Today is a sunny day")[0]
```


```
embeddings = [get_sentence_embedding(sentence) for sentence in sentences]
for embedding, sentence in zip(embeddings, sentences):
	similarity = util.pytorch_cos_sim(query_embedding, embedding)
	print(similarity, sentence)
```



When to use each pooling strategy? It depends on the task.
• [CLS] pooling is usually used when the transformer model has been fine-tuned on a specific
downstream task that makes the [CLS] token very useful.
• Mean pooling is usually more effective on models that have not been fine-tuned on a downstream task. It ensures that all parts of the sentence are represented equally in the embedding and can work for long sentences where the infuence of all tokens should be captured.
• Max pooling can be useful to capture the most important features in a sentence. This can be very useful if particular keywords are very informative, but it might miss the subtler context. 

In practice, a pooling method will be stored with the model, and you won’t have to worry about it. If there’s no method specified, mean pooling is usually a good default.

# SBert document

![[Pasted image 20240722143155.png]]

