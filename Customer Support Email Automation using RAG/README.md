# AI Customer Support Agent using RAG

## Description

This project is an AI-powered customer support chatbot built using **n8n, OpenAI, Pinecone, and Retrieval-Augmented Generation (RAG)**.

The system allows users to ask questions and receive accurate answers based on information stored in uploaded documents. Documents are automatically processed, split into smaller chunks, converted into embeddings, and stored in a Pinecone vector database. When a user asks a question, the AI retrieves the most relevant information from the vector database and uses it to generate the response.

## Architecture

```text
                 Knowledge Base
                       │
                       ▼
                ┌──────────────┐
                │ Google Drive │
                └──────┬───────┘
                       │
                       ▼
                ┌──────────────┐
                │ Download File│
                └──────┬───────┘
                       │
                       ▼
                ┌──────────────┐
                │ Data Loader  │
                └──────┬───────┘
                       │
                       ▼
        ┌────────────────────────────┐
        │ Recursive Character        │
        │ Text Splitter              │
        └─────────────┬──────────────┘
                      │
                      ▼
              ┌────────────────┐
              │ OpenAI         │
              │ Embeddings     │
              └───────┬────────┘
                      │
                      ▼
              ┌────────────────┐
              │ Pinecone       │
              │ Vector Store   │
              └───────┬────────┘
                      │
                      │ Relevant Context
                      ▼
User ──► Chat Trigger ──► AI Agent
                            │
                ┌───────────┼───────────┐
                ▼           ▼           ▼
           Pinecone     OpenAI Chat   Simple
             Tool          Model      Memory
                │           │           │
                └───────────┼───────────┘
                            ▼
                       AI Response
