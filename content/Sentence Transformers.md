SBert user guide blogpost ->  https://huggingface.co/blog/train-sentence-transformers#loss-function

SBert documentation -> https://sbert.net/


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