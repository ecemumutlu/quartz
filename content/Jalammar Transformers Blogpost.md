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


