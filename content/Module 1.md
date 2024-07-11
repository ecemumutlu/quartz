[[Coursera Deep Learning Spec Course Module 1.pdf]]


![[Pasted image 20240705141226.png]]


![[Pasted image 20240705141135.png]]

![[Pasted image 20240705142046.png]]


![[Pasted image 20240705143121.png]]


![[Pasted image 20240705150108.png]]

![[Pasted image 20240705150327.png]]

![[Pasted image 20240705152459.png]]


![[Pasted image 20240708093340.png]]


![[Pasted image 20240708094444.png]]


![[Pasted image 20240708094723.png]]


![[Pasted image 20240708095346.png]]


![[Pasted image 20240708095857.png]]

![[Pasted image 20240708100846.png]]


![[Pasted image 20240708101627.png]]

 - binary classification taskları için last layerda sigmoid, hidden layerlarda ReLU kullan
 - almost never use sigmoid function except for last layer -> for large and small values of x, learning is small since gradient becomes too small -> tanh could be used instead
 - ReLU a = max(0, z) veya leaky ReLU a = max(0.01z, z)  kullan 
 
![[Pasted image 20240708102141.png]]


 - Linear activation function'ı 1 case hariç hiçbir yerde activation function olarak kullanmıyoruz çünkü linear activation function öğrenememeye sebep oluyor. Here is why:
	 - ![[Pasted image 20240708104111.png]]
 - Linear activation function şu casede kullanılabilir:
	 - y is an element of Real number [-inf, inf] 
	 - sadece output layerda linear activation olacak, hidden layerlarda ReLU, tanh vs olacak


![[Pasted image 20240708104911.png]]


![[Pasted image 20240708105120.png]]

![[Pasted image 20240708105331.png]]

![[Pasted image 20240708105944.png]]

![[Pasted image 20240708110505.png]]



![[Pasted image 20240708113117.png]]

![[45023.jpg]]
![[Pasted image 20240708115854.png]]



![[Pasted image 20240708121106.png]]

Do not initialize weights to 0 -> no learning at all


![[Pasted image 20240709102203.png]]


![[Pasted image 20240709103609.png]]

![[Pasted image 20240709103805.png]]

It is perfectly okey to have a for loop to calculate activation functions when there are more than one hidden layers.

![[Pasted image 20240709110521.png]]

![[Pasted image 20240709111409.png]]

![[Pasted image 20240709112558.png]]

![[Pasted image 20240709113516.png]]

cache $Z^{[l]}, W^{[l]}, b^{[l]}$ to be used in backward propagation

![[Pasted image 20240709114442.png]]

![[Pasted image 20240709115453.png]]

