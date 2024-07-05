## Potential Read Path
- [x] [[1-instruction-following.pdf]] 
- [ ] [[2-llama1.pdf]]
- [ ] [[3-llama2.pdf]]
- [x] [[4-lms_are_few_shot_learners.pdf]] + https://www.youtube.com/watch?v=SY5PvZrJhLE&t=1888s&ab_channel=YannicKilcher (first 30 minutes)
- [ ] [[5-lms_are_unsupervised_multitask_learners.pdf]]
- [ ] 6-llama3
- [x]  https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/ 
	- [x] A friendly introduction to Recurrent Neural Networks: https://www.youtube.com/watch?v=UNmqTiOnRfg
- [ ] https://jalammar.github.io/illustrated-transformer/
- [ ] jury paper
- [ ] BERT paper



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