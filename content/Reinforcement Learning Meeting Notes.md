Öyle bir agent üret ki reward max olsun

![[Pasted image 20240710112505.png]]

### Problems
Exploration vs Exploitation
	Agent ne kadar çok yeni şey denemeli veya ne kadar bildiği şeyleri yapmalı -> deneyim kazanırken bunu belirlemek lazım
Correlated Data
	Ceza aldığın case in prerequisite i varsa ikisi correlated oluyor
Reward Attribution
	Neye reward verileceğine karar vermek önemli


PPO -> hem policy hem value öğreniliyor

Motivations
Discete data cannot be differentiable -> loss function cannot be used for these cases

Reward modeling -> Fake human preference


RL de 2 tane Value function var
State Value (V):
	V(S): Bu stateden sonraki tahmini reward
Action-Value (Q):
	Q(S,A): Bu statede bu action'ı alırsam tahmini reward

Advantage (A):
	A(S,A): Q(S,A) - V(S)

