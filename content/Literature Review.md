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


### Jalammar Attention Blogpost
 - Attention mechanism visualization: [[seq2seq_7.mp4]]