## ai agents and function-calling

I recently saw this meme on LinkedIn [here](https://www.linkedin.com/posts/hamelhusain_dont-repeat-this-mistake-you-have-been-activity-7273119135293710336-SnEj?utm_source=share&utm_medium=member_desktop),

![image](https://github.com/user-attachments/assets/2eac474f-4fca-4c80-9b72-de7045757012)

I do have something to say about the right part of the post.

In my opinion, the agentic approach definitely includes function calling. It's not entirely different.  

While the author of the post seems to convey the similar notion, the meme, however, suggests that AI agents and function calling differ a lot. Sure, agents sound cooler than function calling. :P  

Function calling involves configuring and giving the llm the configuration.  
Agents, on the other hand, are about more orchestration—API calls, aka function calls, decision-making, and deciding how the processing should unfold next.

Function calling is used to make the llm’s answer more sound, better suited, factual, or bespoke based on the tools we give it, and also giving the llm the option to decide whether to execute or not.  
The agentic approach comes into play when, based on the llm’s response, we perform an action. For sure, an agent will be written with a toolkit or tools in mind, but it doesn’t differ that much—it's mostly about the orchestration.

For example, imagine you're struggling to manage Jira, so you configure a setup to modify tickets with the help of an llm.  
The modification part is the agentic approach's nuance. Now, if you're just using function calls to check if a ticket needs to be updated, that’s one thing—but agentic takes it further by configuring the next step or action based on the llm’s response.

Quoting Occam's Razor: "Explanations that posit fewer entities, or fewer kinds of entities, are to be preferred to explanations that posit more."  
In other words, if an agentic approach introduces unnecessary complexity without offering significant benefits, it might be more efficient to opt for a simpler solution, like function calling.

I might have perceived the meme incorrectly, which led to this post, but hey, I thought I'd share anyway!
