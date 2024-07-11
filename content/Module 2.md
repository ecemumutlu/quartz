# Week1

## Bias and Variance

![[Pasted image 20240711101437.png]]

![[Pasted image 20240711101742.png]]

## Regularization


variance ->  L2 and L1 Regularization
![[Pasted image 20240711103111.png]]





![[Pasted image 20240711103321.png]]

![[Pasted image 20240711103652.png]]


Frobenius Norm
Weight decay

### How regularization prevents overfitting?

How does regularization prevents overfitting
	lambdanın değerine göre (gerçekten büyük olması durumunda) w weight matrix i daha fazla 0 a yakın değerler içermeye başlıyor. Bu neural networkte bazı değrleri sıfırlıyor yani aynı layer sayısında ama her layerda daha az feature olan bir neural networkle karşılaşıyoruz. Daha simple bir neural networkü traşn ediyor gibi oluyoruz.

![[Pasted image 20240711104554.png]]

For example when activation function is tanh.

When lambda is big -> W will be small -> Z will be relatively small -> small z values end up being nearly linear for tanh function -> in the linear case overfitting will be prevented

## Dropout

Dropout
	with some probability zeroing out some hidden layers while training -> this way it makes us use a smaller network -> regularization effect
	no dropout on the test time 

![[Pasted image 20240711110424.png]]

### Why dropout works?

With dropout inputs can be eliminated. yani o node a gelen inputlardan herhangi birine daha fazla odaklanmasını engelliyor ve weighti daha iyi dağıtabiliyor.

Farklı layerlarda farklı dropoutlar kullanılabilir. Daha az node u olan layerlarda droput kullanılmasa bile olur.


![[Pasted image 20240711111952.png]]


## Augmentation
![[Pasted image 20240711143600.png]]


## Early Stopping

![[Pasted image 20240711143439.png]]

Instead of early stopping l2 regularization can be used but L2 is costly.

## Normalization 

Normalization is used to speed up the training
Subtract mean -> move the training set until it has zero mean
Normalize variances -> so that x and y will reside on the same intervals

![[Pasted image 20240711143939.png]]

### Why normalize inputs?
Normalized Loss function may results in faster gradient decrease with less steps to the minimum

![[Pasted image 20240711144207.png]]

## Vanishing/Exploiding Gradient Problem
Özellikle deep neural networklerde daha da sıkıntılı bir problem
![[Pasted image 20240711150359.png]]

### Solution: Better Weight Initialization

$W^{[l]}$ has $n^{[l-1]}$ input features.
While randomly initializing weights, we normally multiply the values with 0.01. But instead multiplying with variance is better.

Farklı activation functionlar için farklı initialization stratejileri uygulanabilir. Bu aşağıdaki çözümler vanishing/exploiding gradient problemini çözüyor.
![[Pasted image 20240711151202.png]]
