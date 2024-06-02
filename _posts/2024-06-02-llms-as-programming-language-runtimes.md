---
layout: post
title: LLMs as Programming Language Runtimes, or Why Monolithic Text Prompts Are a Mistake
---

## Prompts Are Programs
Fundamentally, LLMs function as a form of language runtime environment. While they might be unpredictable and challenging to reason about, the underlying pattern of program -> output is the same. This connection isn't so obvious when working with chatbots, but as LLMs improve in structured output and function calling, your prompt will define a multi-system computation graph just like any other program, and as LLMs get more tightly integrated into systems this connection will become increasingly important.

Viewing LLMs this way is very helpful for thinking about the engineering around them. One thing that becomes immediately obvious is that using a single text prompt that combines both instructions and user data is a very bad idea. As these systems become more capable, prompt injection could cause serious damage. Unlike traditional systems, where you can be 100% sure you've mitigated a vulnerability, the fuzzy nature of LLMs means you will always potentially be vulnerable to a carefully crafted malicious context.

## Mixing Code and Data Is a Bad Idea
You might be thinking, "If monolithic text prompts are such a bad idea, how should we interact with the model?" My solution is to split the prompt into instructions and data and retrain models to understand the distinction. Not only does this mitigate a major attack vector, but it also unlocks a new form of prompt optimization. Instead of using text for the instructions, the model could take an instruction embedding.  The benefit of this is that instead of having to manually do black magic prompt optimization, you can just have an agent do gradient descent in embedding space to optimize the instruction embedding for an objective function.

Embeddings can be quite lossy, so giving the model an embedding of the data might reduce performance. However, the instruction portion of most prompts can be accurately captured via embeddings, making this approach viable, and we can always develop better embedding methods if needed. Finally, having separate data and instructions has the potential to reduce the instruction-following dilution that currently occurs with extremely long prompts.

Implementing this split doesn't have to be difficult. The naive approach of rewriting the prompts used for task training and fine-tuning models using that new instruction format is a solid start. However, to reap the full benefits, updating attention to treat instructions and data differently will be necessary.

## Reframing Common Techniques
This perspective also recasts many common techniques used with LLMs to improve accuracy as existing engineering tools with a long history. For instance, the techniques of having the LLM check its work and correct it at the end, or having the model answer from multiple perspectives and select the intersection answer can be seen as forms of error-correcting codes.  These prompting techniques are rudimentary but they work, and they suggest that we can do much better if we approach the problem in a principled way.

## Conclusion
I encourage you to adopt the mindset that these models are fuzzy language runtimes. This perspective can help reveal relevant prior work and suggest new directions for inquiry based on what has been successful in analogous systems.

For instance, consider runtime optimization - could we apply traditional runtime optimization techniques to improve the efficiency and performance of LLMs?  Imagine a JIT optimizer that can update model structure to improve inference speed under certain conditions.  Something like that would probably require a model trained to be "modular" and robust to subnetworks being turned on/off at runtime, but it's an interesting idea.  We already have mixture of experts models with routing capability, it wouldn't be a stretch to increase the modularity of the networks and have an optimizer agent that learns from model inputs/outputs in order to situationally de-activate low impact modules based on execution statistics.


