## Potential Read Path
- [x] [[1-instruction-following.pdf]] 
- [x] [[2-llama1.pdf]]
- [ ] [[3-llama2.pdf]]
- [x] [[4-lms_are_few_shot_learners.pdf]] + https://www.youtube.com/watch?v=SY5PvZrJhLE&t=1888s&ab_channel=YannicKilcher (first 30 minutes)
- [ ] [[5-lms_are_unsupervised_multitask_learners.pdf]]
- [ ] 6-llama3
- [x]  https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/ 
	- [x] A friendly introduction to Recurrent Neural Networks: https://www.youtube.com/watch?v=UNmqTiOnRfg
- [x] https://jalammar.github.io/illustrated-transformer/
- [ ] jury paper
- [ ] BERT paper
- [x] GQA:  https://medium.com/@raisomya360/demystifying-sliding-window-grouped-query-attention-a-simpler-approach-to-efficient-neural-6fb03b7d021f
- [ ] [[7-SentencePiece.pdf]]
- [x] Byte-pair encoding: https://www.geeksforgeeks.org/byte-pair-encoding-bpe-in-nlp/



## Key points

### Instruction following [[1-instruction-following.pdf]] 
- **keywords:** Human labelers, GPT3, PPO
- Figure 2 ![[Pasted image 20240702165146.png]]

### LLMs are few shot learners [[4-lms_are_few_shot_learners.pdf]] , [[6-Language_Models_are_Few-Shot_Learners.pdf]]
- I skim through the paper. I especially get the idea of how gpt3 is trained with x-shot settings.

- Figure 2.1 : How gpt3 is trained with zero-shot, one-shot, few-shot settings:
	- ![[Pasted image 20240702170151.png]]
	- Given:
		- Task description
		- One or more examples ( ... -> ...)
		- Prompt (... -> ?)


### [Jalammar Attention Blogpost](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)
 - Attention mechanism visualization: [[seq2seq_7.mp4]]
 - Encoder decoder yapıları kendi içlerinde bir RNN
 - Attention mekanizması özelinde encoder ın her statinde üretilen hidden state değerleri decoder a input olarak veriliyor. Bu hidden state değerleri encoder'ın her bir kelime için attention değerlerini içeriyor.
 - Decoder ilk EOS tokenini input olrak alıyor. Her bir time intervalda bir önceki hidden state outputu ile encoder hidden state değerlerini kullanarak decode ediyor.
 - 

### [Jalammar Transformers Blogpost](https://jalammar.github.io/illustrated-transformer/)
 - 6 encoder + 6 decoder
 - Each encoder is the same in the structure yet they do not share weights
 
 #### **Steps**
 Given a sentence S = {$w_1, ..., w_n$}
  1. Calculate vector embedding $x_n$ for each $w_n$ 
  2. Sum $x_n$ with positional embedding = $z_n$
  3. Calculate query, key, value vectors $q_n, k_n, v_n$ for each $z_n$
	  1. ![[Pasted image 20240705092432.png]]
  4. Calculate score of each position $z_n$ by the following formula
	  1. $softmax( \frac{Q x K^T}{\sqrt{d_k}} ) V$ = Z
	  2. ![[Pasted image 20240705092507.png]]
  5. Assume we applied all above in a multi-head attention manner with 8 heads. We will obtain 8 different Z matrices. We concat them and multiply with an additional weight matrix $W^o$ 
	  1. ![[Pasted image 20240705092347.png]]
  6. Transform last encoders output into K and V and feed into each of the decoders.
  7. Using the K and V first cycle produces and output. After the first cycle, each cycle begins with the previous output. Decoding phase ends when EOS token is produced.
  8. The last layer of decoder outputs a vector of floats of size 1x512. The linear layer and softmax function at the end produces a huge logits vector of size our vocabulary. The cell with the highest probability is chosen to be the corresponding word.
	  1. ![[Pasted image 20240705094129.png]]


### [[2-llama1.pdf | Llama-1]]
 - Llama 1 is trained on a publicly available text data. 
	 - ![[Pasted image 20240708150958.png]]
 - "Recent work from Hoffmann et al. (2022) shows that, for a given compute budget, the best performances are not achieved by the largest mod- els, but by smaller models trained on more data." -> ulaşmaya çalıştıkları bu
 - **Tokenizer:**  We tokenize the data with the [byte-pair encoding (BPE) algorithm](https://www.geeksforgeeks.org/byte-pair-encoding-bpe-in-nlp/)  (Sennrich et al., 2015), using the implementation from [[7-SentencePiece.pdf|Sentence-Piece]]  (Kudo and Richardson, 2018). Notably, we split all numbers into individual digits, and fallback to bytes to decompose unknown UTF-8 characters.
 - Architectural Decisions:
	 - **Pre-normalization [GPT3].** Normalde her her bir encoder decoder layer için sublayer ların son aşamasında output normalization yapılıyor. Bunun yerine her bir sub-layerın inputunu normalize etmişler #ask -> Ben burayı anlamadım yani ilk sublayer inputunu da normalize etmek dışında bir farklılık yapılmamış aslında??
	 - **SwiGLU activation function [PaLM].** Instead of ReLU, SwiGLU activation function is used to improve performance 
	 - **Rotary Embeddings [GPTNeo].** We remove the absolute positional embeddings, and instead, add rotary positional embeddings (RoPE)
 - Optimizer: AdamW
 - Multihead attention kullanmışlar
 - Efficiency artırmak için decoderda kullanılan masked self attention mekanizmasında 0 olan weightleri storelamamışlar
 - To further improve training efficiency, we reduced the amount of activations that are recomputed during the backward pass with checkpoint. More precisely, we save the activations that are expensive to compute, such as the outputs of linear layers. This is achieved by manually implementing the backward function for the transformer layers, instead of relying on the PyTorch autograding.  #ask 
 - Pre-train yaptıktan sonra zero-shot ve few-shot learning ile çeşitli tasklar üzerinde llama skorlarını paylaşmışlar
### [[3-llama2.pdf | LLama-2]]
 - GQA: grouped-query-attention
	 - tüm kelimelere tek tek bakmak yerine kelimeleri öncesinde gruplayıp sadece istediğim grupla alakalı olan kelimelerde attention arıyorum
 - LLama2 ve LLama1 arasındaki farklar:
	 - ![[Pasted image 20240708152259.png]] 
	 - We use the standard transformer architecture (Vaswani et al., 2017), apply pre-normalization using RMSNorm (Zhang and Sennrich, 2019), use the SwiGLU activation function (Shazeer, 2020), and rotary positional embeddings (RoPE, Su et al. 2022). The primary architectural differences from Llama 1 include increased context length and grouped-query attention (GQA).