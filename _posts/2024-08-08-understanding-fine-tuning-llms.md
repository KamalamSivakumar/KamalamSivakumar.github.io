## notes on llm fine-tuning methods: rlhf

Starts with rlhf, this series of blog posts that would cover my notes about preference learning methods.

**RLHF: Reinforcement Learning based on Human Feedback**  
**Motivation**: better evaluation leads to better fine-tuning and thus better results.  
Existing evaluation methods such as [BLEU](https://en.wikipedia.org/wiki/BLEU) and [ROUGE](https://en.wikipedia.org/wiki/ROUGE_(metric)) use algorithms that look at rules and metrics based on parts of sentences, like unigrams and bigrams.  
how about fine-tuning based on feedback from humans?  
**Basic Idea**: pre-train the model --> build reward model based on human feedback --> fine-tune with reinforcement learning  
**My understanding of how it works**:  
**(pre-trained model)**  
Start with a basic pre-trained model. This model can be augmented with guardrails or tuned for specific conditions, but it doesn’t have to be—just having a model that can respond to instructions is essential.  
A model that's already fine-tuned to some extent can enhance the rlhf fine-tuning method, much like how setting the learning rate hyperparameter affects the optimization algorithm.

**(sft)**  
Generating the reward model involves numerically representing human preferences, i.e., should take in a response and give a metric that resonates human preference.  
The reward model may be a language model attuned to preferences or a language model pre-trained just on preferred data.  
(prompt, response) is needed to build the reward model. Human annotators are used to rank the generated responses from the language models. (Rank instead of score, cause the reward model would then become very noisy/varied, making it very sensitive. Rank to get a regularized dataset.)  
Different methods of ranking are normalized into a scalar reward signal for training. (example method of ranking: [Elo rating system](https://en.wikipedia.org/wiki/Elo_rating_system), ranking relatively based on responses from 2 language models for the same prompt.) (interesting this elo system is, read it!)  
Reward language models need to have similar capacity to understand the text given to them as a model would need in order to generate said text.

**(rlhf - using rl)**  
Using RL to optimize the language model with respect to the reward model.  
What multiple organizations seem to have gotten to work is fine-tuning some or all of the parameters of a copy of the initial language model with a policy-gradient RL algorithm (will explain it below), [Proximal Policy Optimization (PPO)](https://huggingface.co/blog/deep-rl-ppo). 
Some parameters of the language model are frozen because fine-tuning an entire 10B or 100B+ parameter model is really expensive, even for mammoth organisations. (lora comes into play here, will explore it in a separate post)  
**policy**: mapping from perceived states of the environment to actions to be taken (in our case the language model taking in a sequence of texts and giving a sequence of texts. (basically giving the probability distributions over the text))  
**action space/states**: the set of all valid actions, or choices, available to an agent as it interacts with an environment (in our case the all possible tokens)  
**observation space**: the set of all valid inferences available to an agent based on its action space/state (in our case distribution of possible input token sequences)  
**context of reward function**: for the agent to learn an optimal, or nearly-optimal, policy that maximizes the "reward function" (in our case learn to respond like humans)  

Given the prompt "x", the response "y" is generated based on the current policy iteration.  
The preference model would return the score "r", for the input (x,y)  
The distribution of probabilities from the current policy iteration i.e., the current language model is compared with the initial language model, to compute a penalty, kinda like the loss function in conventional sense.  
In multiple papers from OpenAI, Anthropic, and DeepMind, this penalty has been designed as a scaled version of the Kullback–Leibler [KL-divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence) (KL Divergence is a way to measure how different these two sets of predictions are from each other. KL divergence is like a score that shows how much one model's idea of what should come next differs from another model's idea. Score would be low for similar distributions.)    
The KL divergence term penalizes the RL policy from moving substantially away from the initial pre-trained model with each training batch, which can be useful to make sure the model outputs reasonably coherent text snippets. Without this penalty the optimization can start to generate text that is gibberish but fools the reward model to give a high reward. (hallucinations handled? yep.)  
The final reward is: r - kl_coeff*r_kl (r_kl --> kl penalty, kl_coeff --> scale of the kl penalty (hyperparam))  

Finally, update rule: PPO that maximizes the reward metrics in the current batch of data.  
PPO is on-policy, which means the parameters are only updated with the current batch of prompt-generation pairs.  
PPO uses constraints on the gradient to ensure the update step does not destabilize the learning process.  
RLHF can continue iteratively updating the reward model and the policy together. As the RL policy updates, users can continue ranking these outputs versus the model's earlier versions.

This is the basic idea, but other than this other methods can be applied to improve the preference learning aspect. (like dpo, orpo; will write separate posts)

**References**:  
[RLHF - Huggingface](https://huggingface.co/blog/rlhf) -- This is such a good post to learn rlhf from. I'll also need to look into the hyperlinks mentioned in the notes to get a fuller understanding.  
[RLHF - Chip Huyen](https://huyenchip.com/2023/05/02/rlhf.html) -- Her explanations and analogies are great for understanding. 
