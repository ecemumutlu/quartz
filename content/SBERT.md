 - paper link: [[15-sbert.pdf]]
 - blogpost link: https://towardsdatascience.com/sbert-deb3d4aef8a4
 - Sbert.net documentation/library usage : https://sbert.net/

## Useful links
 - [[Bi-encoders vs. Cross-encoders]]
 - [[Sentence Transformers]]
 - [[BERT]]

## Model Architecture
 - SBERT adds a pooling operation to the output of BERT / RoBERTa to derive a fixed sized sentence embedding.

![[Pasted image 20240725144210.png]]
 - Non-Siamese (cross-encoder) architecture is shown on left, and the Siamese (bi-encoder) architecture is on the right. The principal difference is that on the left the model accepts both inputs at the same time. On the right, the model accepts both inputs in parallel, so both outputs are not dependent on each other.

### Objective Functions
#### Classification Objective

 - Finally, three vectors _u_, _v_ and _|u-v|_ are concatenated, multiplied by a trainable weight matrix _W_ and the multiplication result is fed into the ==softmax classifier== which outputs normalised probabilities of sentences corresponding to different classes. 
 - The ==cross-entropy loss function== is used to update the weights of the model.
 - #ask burada nasıl labellar verdiklerini göremedim. Yani NLI gibi mi incelemişler burayı it follows it does not follow vs gibi?
 - ![[Pasted image 20240725151243.png]]
![[Pasted image 20240725151043.png]]
#### Regression Objective Function
  - In this formulation, after getting vectors u and v, ==the similarity score between them is directly computed by cosine similarity.== 
  - The predicted similarity score is compared with the true value and the model is updated by using the ==MSE loss function.== 
  - ![[Pasted image 20240726095030.png]]
  - #ask şimdi burada loss hesaplarken predicted value true value ile karşılaştırılıyor diyor. True value yu nereden buluyoruz?
  - ![[Pasted image 20240725151357.png]]


#### Triplet Objective Function
 - The triplet objective introduces a triplet loss which is calculated on three sentences usually named ==_anchor_====, ==_positive_== ==and== ==_negative_====. 
 - It is assumed that _anchor_ and _positive_ sentences are very close to each other while _anchor_ and _negative_ are very different. 
 - During the training process, the model evaluates how closer the pair ==_(anchor, positive)_== is, compared to the pair ==_(anchor, negative)_====.
 - **The triplet SBERT architecture differs from the previous two in a way that the model now accepts in parallel three input sentences (instead of two).**
 - Loss function:
	 - ![[Pasted image 20240725151643.png]]
 - ![[Pasted image 20240725151704.png]]
 - 