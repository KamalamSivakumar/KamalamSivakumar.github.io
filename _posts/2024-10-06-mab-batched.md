## reinforcement learning - multi-arm-bandits and batched bandit problem

This post is about the batched bandit problem, as background research.  
All of this is part of my ongoing effort to fully grasp the concepts presented in the pre-print. [Sarvesh Gharat et al](https://arxiv.org/abs/2408.14195)

**Bandit problem**:  
[multi-armed-bandit repo](https://github.com/KamalamSivakumar/Multi-arm-Bandit)  
It's named after the scenario where a gambler faces a row of slot machines/arms (or "one-armed bandits") and must decide which machine/arm to play (or "pull") to maximize their total reward over time.  
The point of bandit algorithms is to balance exploring the possible actions and then exploiting actions that appear promising.  

**Batched Bandit problem**:  
Why batched? [Perchet et al](https://arxiv.org/pdf/1505.00369)  
Clinical trials, typically conducted in batches with patient data influencing subsequent designs, can be optimized using the multi-armed bandit framework.  
>> At each point in time
t = 1,...,T , a decision maker chooses to sample one, and receives a random
reward dictated by the efficacy of the treatment. The objective is to devise a series of choices—a policy—maximizing the expected cumulative reward over T
rounds.

In real-world scenarios - Not receiving instantaneous rewards, but rather get rewards for actions done in batches/over a time frame.  

**Grid**:  
**Arithmetic Grid**:  
evenly divides the time horizon T into M equal batches.  
when M=T, this is equivalent to the traditional bandit problem with instant rewards.  
Static Grid: fixed in advance || Adaptive Grid: the next grid point is based on historic data.  
Attaching notes.  

![Batched Bandit Problem](https://github.com/user-attachments/assets/e6392aec-f07f-4431-a2ae-edd28554cc4b)

**Traditional Bandit Problems --> Batched Bandit Problems**  
The difference between the batched bandit and the regular bandit is when the agent is allowed to update the policy.  
Wait until the end of the batch to update the agent's policy.  

More to learn on this:  
Minimax Grid, Geometric Grid, Batched Successive Elimination (BaSE), How all of this is applied?

**References**:  
[Batched bandit problems - Perchet et al](https://spia.princeton.edu/system/files/research/documents/Chassang_Batched%20Bandit%20Problems.pdf)  
[Batched bandit problems - Sean Smith Medium blog](https://towardsdatascience.com/batched-bandit-problems-ea73dba5da7a)
