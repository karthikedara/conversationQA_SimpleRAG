# ConversationQA_SimpleRAG

This is a simple RAG application which takes input from a website and creates the Chroma vector DB and using the tensorflow library it remebers the previous chat history based on the session id and everytime the model is called the context of the chat history and the documents will be sent to the model

```mermaid
graph LR
    subgraph "Data Plane (VPC / On-Premise)"
        A[Data Sources: Git, Confluence, Slack, etc.] --> B(Data Ingestion & Processing Layer)
        B -- Chunks & Embeddings --> C[Vector Database: ChromaDB/Pinecone]

        D[Chat Interface: Slack/Web App] --> E[Orchestration API: LangChain/LlamaIndex]
        E -- User Query --> F[1. Retriever]
        F -- Embeds Query --> C
        C -- Returns Relevant Chunks --> F
        F -- Context --> G[2. Generator]
        E -- User Query + Context --> G
        G -- Formats Prompt --> H
        H -- Synthesized Answer --> G
        E --> D
    end
