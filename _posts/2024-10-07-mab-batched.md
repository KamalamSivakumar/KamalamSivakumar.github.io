## reinforcement learning - multi-arm-bandits and batched bandit problem - part 2

Learning to understand the preprint - Representative Arm Identification: A Fixed Confidence Approach to Identify Cluster Representatives,  
The goal in Representative Arm Identification is to reliably identify a certain prespecified number of arms from each cluster while using
as few arm pulls as possible.  

Objectives while interacting with MAB,  
--maximize the expected cumulative reward accrued over a certain time horizon.  
--minimize the regret with respect to an oracle that knows the arm reward distributions beforehand.  
--typically based on the idea of balancing exploration (trying different arms to reduce uncertainty about their mean rewards) and exploitation
(pulling the arms known to have high rewards).  
--identifying the best arm in terms of the mean reward. (fixed confidence and fixed budget setting)  
--fixed confidence: the goal is to find the best arm using the minimum number of pulls while guaranteeing a certain pre-specified error probability.  
--fixed budget: the total number of pulls is fixed beforehand and the aim is to minimize the probability of error.  

**Pure exploration problems**:  
Focus is on acquiring information about the environment, rather than immediate reward maximization.  
The agent's goal is to explore the environment thoroughly to reduce uncertainty about the possible actions' outcomes.  
For tasks where a set of optimal actions requires extensive exploration before exploitation.  
The focus is entirely on exploration, as exploitation of known information is deferred until after the environment is well understood.  

**Representative Arm Identification Problem**:  
Objective relaxed problem i.e., MAB problems with multiple correct answers.  
A general lower bound on the sample complexity and an asymptotically optimal (as error probability δ → 0) algorithm are provided.  
The goal: identify "representative arms from each cluster, while using as few arms as possible"  

Attaching the corresponding notes, typing got difficult.  

![20241008_175908](https://github.com/user-attachments/assets/235b4eb7-d71d-4365-bd9d-79e163f11192)

![20241008_175914](https://github.com/user-attachments/assets/a261f258-45ba-4381-ac9b-9d1d72c56b6c)

To be continued.  

**Reference**:  
[Gharat et al](https://arxiv.org/abs/2408.14195)
