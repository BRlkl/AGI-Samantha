## Samantha from the movie Her is here: 

An autonomous agent for conversations capable of freely thinking and speaking, continuously. Creating an unparalleled sense of realism and dynamicity.

## Features:

-Dynamic speech: Samantha can speak whenever it chooses to, influenced by its context, in stark contrast to normal LLMs which are limited to answering and reacting. It is also not limited to solving tasks, like all other autonomous agents.

-Live visual capabilities: Visuals are only mentioned and acted upon directly if relevant, but always influences thoughts and behavior.

-External categorized memory: Gets dynamically written and read by Samantha, which chooses the most relevant information to write, and to retrieve to context.

-Evolving at every moment: Experiences that get stored in the memory can influence and shape subsequent Samantha behavior, like personality, frequency, and style of speech, etc.

## How to use:

You communicate with Samantha on the terminal while you can see its inner workings on the flask website. 

Speak or type "Stop" to stop the agent and save its state.

Be sure to plug in OpenAi API and ElevenLabs API (If you want TTS).

Keep in mind that as it currenly stands, the system is relatively slow and very expensive

## How it works:

Orchestration of a collection of LLM calls each with a different purpose. I call each specialized LLM call a “Module”. Samantha is not a single module, but the sum of them, all working together.

There are the following modules: Thought, Consciousness, Subconsciousness, Answer, Memory_Read, Memory_Write, Memory_Select. Alongside Vision. Each of them with a different system prompt, and their inputs and outputs orchestrated among themselves to simulate a basic human brain workflow.

In short, the agent is a never-ending loop of thoughts and auxiliary systems, constantly receiving visual and auditory stimuli, and based on all that it decides what, when and if to say something. 

![Screenshot_119](https://github.com/BRlkl/AGI-Samantha/assets/63427520/253edb6f-74d2-4903-aac7-58fc3b28d535)

The following pipeline is repeated indefinitely:
A loop iteration begins with a gpt-4Vision. The subconsciousness module then processes visual and user input (User can input at any time), it also analyzes the current context of what is going on and produces a description of Samantha’s feelings and emotions. Then the memory_read gets called to analyze current context and provide only relevant memory for Samantha to keep in her context length. After that, the consciousness module gets called to analyze the context and decide on what Samantha should do, if to speak or to continue thinking, and if so, about what. Then, thought module receives the command from the consciousness module, and produces a rational piece of thought. Finally, if the consciousness module decided to speak, the answer modules receives Samantha’s thoughts and composes an answer the user will see. The memory_write module gets called to transfer information from the Short-Term Memory to the Long-Term Memory only once in a while when the Short-Term Memory length gets above a threshold.

Bellow is a detailed description of the inputs and outputs of each module:

Short-Term Memory is stored as a string in python while the Long-Term Memory a dictionary. The former records what the user says, what Samantha says and her thoughts. The latter groups dense knowledge and information abstracted from the former.

-Thought: Receives as input the Long-Term Memory, Short-Term Memory, Subconsciousness, Consciousness, and the current time. The output will be a unit of a thought (Similar to when LLM is prompted to think step by step, the output of this module is one step)

-Consciousness: Receives as input the Long-Term Memory, Short-Term Memory and Subconsciousness. The output will be a decision on whether to continue thinking or to speak, and if to continue thinking, then it will also say what to think about and why (Prompting it to say why improves coherence).

-Subconsciousness: Receives as input the Long-Term Memory, Short-Term Memory, Subconsciousness alongside visual and textual input. The output will be the summary of the context of what is happening, the visual and textual stimuli (If exists), and the agents’ feelings and emotions about what is happening. 

-Answer: Receives as input the Long-Term Memory, Short-Term Memory and Subconsciousness. The output will be what the agent speaks out loud for the user, made as a composition of its thoughts. 

-Memory_Read: Receives as input the Short-Term Memory and the name of the categories of the Long-Term Memory “Keywords”. Output will be a list of the most relevant categories/keywords given the context of the Short-Term Memory. (Code then feeds the entries in the selected categories to the other modules as the relevant part of “Long-Term Memory”)

-Memory_Select: Similar to Memory_Read but instead of selecting the keywords relevant for the agent to remember given the recent Short-Term Memory, this module selects the keywords relevant for the agent to store new information inside, given the oldest entries in the Short-Term Memory. Output is list of keywords. (Code expands these keywords and feeds Memory_Write).

-Memory_Write: Receives as input the expanded keywords and the Short-Term Memory. Output will be the extended keywords with the additions and modifications made by the module. (Code will then update the Long-Term Memory with the modifications).

## How to improve:

Better results can continuously be achieved by tweaking which modules are present, the organization of the modules, and the prompt of the modules.

Think of a thing that the human mind can do that LLM "Cannot", then implement it, then test it. Easy to do and to iterate. The more that is done the closer it is going to be to the human mind.

But most importantly: Smaller models each trained specifically to do the job of one of the modules will greatly increase quality, and decrease cost and latency.

## Installing dependencies:
`sudo apt install libcairo2-dev`
`sudo apt install libgirepository1.0-dev`
and then:
`pip install -r requirements.txt`

## Running
`python AGI-1.py`

Contact: 
pedroschindler@gmail.com
