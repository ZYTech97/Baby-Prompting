<h1 align="center"> <a href="">Baby Prompting: Allowing Large Language Model Asking</a></h1>

[English](README.md) | [简体中文](README.zh-CN.md)

## Abstract  
Existing large language models (LLMs) respond to virtually any user query with the confident demeanor of an expert, delivering assured answers—even when the question itself may be ambiguous or lack clarity. This characteristic often leads to low-value responses when essential context is missing or the question is ambiguous. We propose the concept of **Baby Prompting**, where LLMs are encouraged to ask users clarifying questions when they do not fully understand the query before generating an answer. This approach enhances question quality, improves interaction efficiency, and saves computational resources. We refer to the behavior of LLMs asking questions as **Baby Behavior**, which allows LLMs to seek clarification from users when needed like a baby. We demonstrate the effectiveness of Baby Prompting through a set of test cases.  

## Introduction  
When using LLMs, a common phenomenon is that they respond confidently to any user query, making it difficult for users to discern whether the response is valid or not. In this paper, we define this behavior—where an LLM provides an answer as if it were an expert, even when the question itself is unclear, but the response does not actually meet the requirements—as **Pretending to be an Expert**. In such cases, users must spend extra time understanding or correcting the LLM's response, which reduces interaction efficiency.  

Researchers have been exploring ways to improve their interaction efficiency, mainly by designing more precise prompts to guide LLMs toward generating more accurate responses. The mastery of prompt engineering has even become a specialized profession. However, as LLMs become more widely used, their users are not necessarily skilled prompt engineers but rather ordinary users who do not want to spend extra time refining prompts. Even as a computer science researcher and an early adopter of ChatGPT, the author rarely spends time crafting detailed prompts, providing rich context, or formulating precise questions. Instead, like most users, I tend to ask straightforward questions and only refine them when the responses do not meet my expectations.  

In human communication, people do not always answer questions directly; they frequently ask clarifying questions to ensure a better understanding before responding. LLMs should also have this capability—when a question is unclear, they should ask the user for clarification before attempting to answer. We refer to this behavior, where LLMs act like a baby by asking clarifying questions when the context is unclear, as **Baby Prompting**. The goal of Baby Prompting is to improve interaction efficiency, reduce user effort, and enhance the overall quality of responses. For ordinary users unfamiliar with prompt engineering, allowing the model to ask clarifying questions can help them refine their queries and ultimately receive more useful answers.  


## Methodology  

Since current LLMs generally lack the ability to ask questions, we need to design a prompting method called **Baby Prompting** to guide them in determining whether a user’s question is clear. If the question is unclear, the model should first ask for clarification before generating an answer. Baby Prompting is still in its exploratory stage, and we propose a simple approach: appending a general instruction after the user’s query. Below are two variations of this prompt:  

```
<User's question>  
If anything in the request is unclear, please do not answer immediately. Instead, ask me for clarification first.  
```  

or  

```
<User's question>  
If any part of the question is unclear, do not proceed with answering. Instead, keep asking questions until you fully understand the query.  
```  

This prompt helps guide LLMs to assess whether a user’s question is clear. If not, they should ask the user for clarification before responding. We demonstrate the effectiveness of Baby Prompting using a set of test cases.  

---

## Testing  

We conducted tests on **DeepSeek** and **ChatGPT**, using the following test cases:  

1. **Without Baby Prompting**  

```
Please write an article about the history of distributed system development.  
```  

2. **With Baby Prompting**  

```
Please write an article about the history of distributed system development. If any requirements are unclear, please ask me questions first instead of attempting to answer the request.
```  


The following demonstrates the effectiveness of Baby Prompting based on test results for ChatGPT and DeepSeek:

- **Final Output Quality:**  
  When using Baby Prompting, both ChatGPT and DeepSeek generate content that structurally resembles human-authored technical articles, with significant improvements in technical depth, article coherence, and linguistic style. In contrast, results generated without Baby Prompting tend to resemble article outlines rather than polished technical writing.  

- **Interaction Efficiency:**  
  Baby Prompting requires only one additional user-model interaction while substantially enhancing output quality. Once user requirements are clarified, ChatGPT and DeepSeek directly generate complete articles without repeatedly soliciting user input.  

- **User Experience:**  
  Baby Prompting requires merely appending a universal prompt to queries. This enables both models to produce professional-grade responses without sophisticated prompt engineering, making it particularly accessible for non-expert users.  


### DeepSeek Test Results  
Without Baby Prompting, DeepSeek generated the following article:  
![Sample Image](./data/DeepSeek_2.png "Example")  

With Baby Prompting, DeepSeek generated the following article:  
![Sample Image](./data/DeepSeek_3.png "Example")  

### ChatGPT Test Results  
Without Baby Prompting, ChatGPT generated the following article:  
![Sample Image](./data/ChatGPT_2.png "Example")  

With Baby Prompting, ChatGPT generated the following article:  
![Sample Image](./data/ChatGPT_3.png "Example")  
