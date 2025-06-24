# Overview

This repo contains code examples of using LangChain. The material follows and extends from following sources
1. [LangGraph Guide](https://langchain-ai.github.io/langgraph/#get-started)
2. [LangGraph: Build Stateful AI Agents in Python](https://realpython.com/langgraph-python/?utm_source=realpython&utm_medium=web&utm_campaign=related-post&utm_content=build-llm-rag-chatbot-with-langchain)

### What's the difference between LangChain and LanGraph?
- LangGraph is an orchestration framework for complex agentic systems (useful for complex chains and retrieval flows)
- LangChain provides a standard interface to interact with models and other components (useful for straight-forward chains and retrieval flows)

# Project Aim
LangGraph email processor that can scan a text file containing a list of emails, extract critical information (e.g. official notice emails) from them and notify the correct internal team who will take action

# Steps to accomplish aim

1. Chain#1 - to extract structured fields from the emails in a structured (JSON) format
    - structured fields will be defined using Pydantic Basemodel through class `NoticeEmailExtractor`
    - context information will be given with a prompt template
    - LangChain will pass the information in the `NoticeEmailExtractor` definition as raw text to an LLM
    -  
2. Chain#2 - to make a determination of whether the notice email requires escalation
    - criteria for escalation is provided with a prompt

The chains above are good examples of `stateless` chains that are good with a give specific task but can't make any conditional decisions e.g. what action to take if an email is determined to require escalation

# Learnings
- LLM did an excellent job of accurately extracting relevant fields using the type hints and description parameters declared in the `NoticeEmailExtractor` class definition and prompt. No type conversion logic was necessary.