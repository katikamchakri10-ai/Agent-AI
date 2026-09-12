# AI-Powered Web Content RAG Chatbot using n8n

An AI-powered Retrieval-Augmented Generation (RAG) chatbot built using **n8n, OpenAI, and Pinecone**.

This project extracts content from the **India Today Technology** website, processes the content, splits it into smaller chunks, generates embeddings using OpenAI, and stores them in Pinecone. An AI Agent retrieves relevant information from the vector database and generates contextual answers to user questions.

## 🚀 Project Overview

This project demonstrates how to build a complete RAG-based AI chatbot using n8n.

The system uses website content as a knowledge source. The content is extracted from the website, converted into documents, split into smaller chunks, transformed into vector embeddings, and stored in a Pinecone Vector Database.

When a user asks a question, the AI Agent searches the Pinecone database for relevant information and uses the retrieved context to generate an answer using the OpenAI Chat Model.

## 🌐 Knowledge Source

India Today Technology:

https://www.indiatoday.in/technology

## 🏗️ Architecture

### Data Ingestion Pipeline

```text
                    ┌─────────────────────┐
                    │    Manual Trigger   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │    HTTP Request     │
                    │   GET Website URL   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │        HTML         │
                    │ Extract Web Content │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │  Default Data Loader│
                    │   Create Documents  │
                    └──────────┬──────────┘
                               │
                               ▼
              ┌──────────────────────────────────┐
              │ Recursive Character Text Splitter│
              │          Create Chunks           │
              └───────────────┬──────────────────┘
                              │
                              ▼
                    ┌─────────────────────┐
                    │  OpenAI Embeddings  │
                    │    Text → Vectors   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │  Pinecone Vector    │
                    │       Store         │
                    └─────────────────────┘

-----------------------------------------------------------------

###RAG Question Answering Pipeline

                    ┌──────────────────────┐
                    │ When Chat Message    │
                    │      Received        │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │       AI Agent       │
                    │   Process Question   │
                    └───────┬───────┬──────┘
                            │       │
              ┌─────────────┘       └──────────────┐
              ▼                                    ▼
    ┌───────────────────┐                ┌──────────────────┐
    │ OpenAI Chat Model │                │  Simple Memory   │
    │ Generate Response │                │ Conversation     │
    └───────────────────┘                └──────────────────┘
                            │
                            ▼
                  ┌─────────────────────┐
                  │ Pinecone Vector     │
                  │       Store         │
                  │ Retrieve Context    │
                  └──────────┬──────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │ OpenAI Embeddings   │
                  │  Query Embedding    │
                  └─────────────────────┘

### RAG Complete Workflow

Website
   ↓
HTTP Request
   ↓
HTML Extraction
   ↓
Default Data Loader
   ↓
Recursive Character Text Splitter
   ↓
OpenAI Embeddings
   ↓
Pinecone Vector Store
   ↓
User Question
   ↓
AI Agent
   ↓
Pinecone Retrieval
   ↓
Relevant Context
   ↓
OpenAI Chat Model
   ↓
Final Answer
