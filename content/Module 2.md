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



# Week2: Optimization Algorithms
Daha hızlı train etmek ve daha hızlı sonuç almak adına optimization algoritmalarını kullanıyoruz.

## Mini-batch
![[Pasted image 20240716084235.png]]


![[Pasted image 20240716084805.png]]



![[Pasted image 20240716085005.png]]

![[Pasted image 20240716085649.png]]


![[Pasted image 20240716085902.png]]

![[Pasted image 20240716090321.png]]

![[Pasted image 20240716090758.png]]



Depending on the $\beta$ , we average over $\frac{1}{1 - \beta}$ days/units

![[Pasted image 20240716094105.png]]

![[Pasted image 20240716094555.png]]

V_0 = 0 introduces a bias that reduces the initial average values



## Gradient Descent with momentum
Gradient descent update kısmında dw'yi farklı updateliyorsun.

![[Pasted image 20240716101302.png]]

![[Pasted image 20240716101551.png]]

soldaki kullanım tercih edilmeli

## RMSProp

Gradient descent update ksımında dw 'yi böleceğin bir değer hesaplıyorsun.

![[Pasted image 20240716102308.png]]



## Adam (Adaptive moment estimation) optimizer

RMSProp + momentum  = Adam


![[Pasted image 20240716103047.png]]


![[Pasted image 20240716103505.png]]


## Learning Rate Decay
decay rate below becomes another hyperparameter

![[Pasted image 20240716103544.png]]
slowly reduce alpha

![[Pasted image 20240716105803.png]]

![[Pasted image 20240716110125.png]]

## Local optima problem
When the derivative is close to 0 for a long time, it slow down the learning -> plateaus
most points of zero gradient in a cost function are saddle points, not local minimums

![[Pasted image 20240716111027.png]]



# Week3: HyperParameter Tuning


![[Pasted image 20240718082724.png]]


![[Pasted image 20240718082734.png]]


![[Pasted image 20240718082858.png]]

Büyük dikdörtgen içinde en iyi perform eden değerleri bulduktan sonra bu noktaları merkeze alarak daha küçük bir dörtgende daha sıkı bir arama yapılabilir.


## Scaling while hyperparameter tuning
![[Pasted image 20240718083522.png]]

mesela learning rate için arama yaparken logaritmik scale'de uniform randomized bir search yapmak daha makul..

Yani $a = log_{10}0.0001 < r < b = log_{10}1$ scalingde r içinbir randomiation yapmalıyız.


![[Pasted image 20240718084001.png]]

Aynı şekilde burada da beta değerinin 0.9 olması ile 0.999 olması arasında çok fark var. 0.9 olması son 10 günlük averagea bakılıyor olması anlamına gelirken 0.999 olması son 1000 günlük average a bakılıyor olmasına denk. Bu durumda 1 - beta üzerinden logaritmik bir randomization uygulanmalı.


# Week3: Batch normalization

![[Pasted image 20240718090142.png]]

eğer sadece z_norm kullanacak olsak hidden unitler için tüm değerler mean 0 ve variance 1 olacaktı. ama belki onlar için farklı bir distribution olması daha anlamlı olabilri.  O yüzden z_norm'u iki parametre ile linearization yaparak z_tilda hesaplıyoruz. 

normalizing z (before activation) is much more preferred to normalizing a (after activation)

![[Pasted image 20240718093603.png]]


Because batch norm zeroes out the mean, if we use batch norm for hidden units, we dont need to learn b parameter. Instead beta parameter is enough
![[Pasted image 20240718094154.png]]

![[Pasted image 20240718094429.png]]



![[Pasted image 20240718100127.png]]


# Week3: multiclass classification

![[Pasted image 20240718105128.png]]


![[Pasted image 20240718113732.png]]
