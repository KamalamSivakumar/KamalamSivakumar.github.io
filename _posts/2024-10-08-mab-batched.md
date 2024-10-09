## reinforcement learning - multi-arm-bandits and batched bandit problem - part 3

An important aspect of the RAI problem: multiple correct answers. 

Goal of the paper: Design δ-probably-correct schemes/algorithms for the RAI problem, whose sample complexity is as small as possible.  

What is a δ-probably-correct algorithm?

![20241009_181133](https://github.com/user-attachments/assets/79ae36b6-9f9b-444a-a693-8e69b6bf48c7)

error-threshold δ & confidence-level (1-δ) :  
--maximum allowable probability that the algorithm's output is incorrect.  
--a smaller δ, say δ=0.01, then the algorithm aims for a high confidence level in its correctness.  
--confidence level: if δ=0.05, then the algorithm is 95% confident that its output is correct.  
δ is a parameter controlling the trade-off between the algorithm's accuracy and its confidence.

Further: Bounds, Algorithms and Case Studies

**Reference**:  
[Gharat et al](https://arxiv.org/abs/2408.14195)
