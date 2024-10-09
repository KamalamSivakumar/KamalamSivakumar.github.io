## heuristics, stochastic modelling, and behaviour modelling 

Really broad overview. 

**Heuristics**:  
--heuristics are problem-solving strategies or techniques that simplify decision-making and facilitate finding satisfactory solutions to complex problems, especially when exhaustive search or optimization is impractical.  
--heuristics enhance the performance of AI systems by providing efficient methods for decision-making, problem-solving, and search, particularly in situations with large state spaces or limited computational resources.  
--heuristics help prioritize promising paths in algorithms like A*, evaluate board positions in chess AI, and influence feature selection in machine learning to improve model performance. They also play crucial roles in natural language processing, reinforcement learning, robotics, and constraint satisfaction problems.  
--are integral to ai (encompasses ml, dl, rl, eda, analytics and nlp)

**Stochastic Processes**:  
--collections of random variables representing systems that evolve over time under uncertainty, used to model unpredictable phenomena in various fields.  
--classified by their time index (discrete/continuous), state space (discrete/continuous), and dependencies (e.g., Markovian, stationary, etc.).  
--A Markov chain is a type of stochastic process where the future state depends only on the present state, not on the sequence of past states.  
--Matrices that describe the probabilities of transitioning from one state to another in a Markov chain, encapsulating the dynamics of the process. (transition probability matrix)  
--MDPs are a framework for decision-making where outcomes are partly random and partly under control, used in optimization and AI.  

**Markov Decision Processes**:  
--consists of states, actions, transition probabilities, and rewards.  
--The objective is to find a policy (a set of actions) that maximizes cumulative rewards over time, often solved using techniques like dynamic programming or reinforcement learning.  
--the system evolves through states based on actions taken by a decision-maker, and these transitions between states are probabilistic.   
--optimal decision-making under uncertainty to maximize cumulative rewards.  

**Hidden Markov Models**:  
--the system is in a hidden state at each time step, and we only observe outputs (emissions) that are probabilistically related to the hidden states. The primary task in HMMs is to infer the most likely sequence of hidden states given the observations.  
--sequence of hidden states given observations (e.g., Viterbi Algorithm).  
--The Viterbi algorithm: Given a sequence of observed events, find the most probable sequence of hidden states that could have generated those events, using dynamic programming to efficiently compute the best path.  

While both are related to probabilistic models, MDPs focus on decision-making, while the Viterbi algorithm is about finding the most likely sequence of hidden states.  

**Behaviour Modelling**:  
--modelling uncertain systems based on a particular pattern or behaviour.  
--queueing theory, decay models, brownian motion, nature-based optimization algorithms. (eg., ant colony optimisation algorithm)

**How does all of the above apply to ai?**  
--in my opinion, all of the above fall under the umbrella of "ai", in addition I'd also say game theory, tradeoffs as well.  
--modeling—whether it involves uncertainty or not—is fundamental to ai.  
--ignoring all the jargons, at a fundamental level, everything we aim to achieve can be categorized as a constraint optimization problem, which can further be viewed as mathematical modeling or stochastic modeling when probabilities come into play.

**References**:
[Course Structure and Reference books mentioned](https://www.psgtech.edu/educms/sorces/AMC/progregs/M.Sc(DS)-2015-Regulations.pdf)
