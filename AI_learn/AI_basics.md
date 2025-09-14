
# AI Basics – Tutorial Notes

These notes cover essential terminology and concepts related to AI applications, Large Language Models (LLMs), and Retrieval-Augmented Generation (RAG).  
They are written for students, tech enthusiasts, and anyone beginning their AI learning journey.

---

## 1. AI Applications and Models

- **AI Application** – A software or service that uses artificial intelligence to respond to user queries or perform tasks.
- **ChatGPT** – An AI chatbot developed by OpenAI. Popular models include GPT-4.0, GPT-4.1, GPT-4o, and GPT-4o mini.
- **Claude** – An AI chatbot developed by Anthropic, powered by models like Claude Sonnet 4, Sonnet 4.1, and Claude Focus 4.1.
- **Google Gemini** – Google’s AI model for chat and reasoning tasks.
- **Generative AI (GenAI)** – A type of AI that generates text, images, or other content based on input prompts.

---

## 2. Large Language Models (LLMs)

- **LLM (Large Language Model)** – The core technology behind most AI applications, trained on massive datasets to predict and generate text.
- **Model Versions** – Examples include GPT-4, GPT-4o, Claude Sonnet 4. These represent different capabilities and context limits.
- **Training Data** – Large collections of text used to train models. Each model has a **training cutoff date** beyond which it has no knowledge.
- **Algorithm** – Mathematical and statistical methods used to train LLMs on data.

---

## 3. Tokens and Context

- **Token** – The smallest unit of text an LLM processes (a word or part of a word).  
  Example: “learning” may be split into `learn` + `ing`.
- **Tokenization** – The process of breaking text into tokens before processing.
- **Context Window / Context Limit** – The maximum number of tokens an LLM can process at once (e.g., 40K, 128K, or 256K tokens).
- **Hallucination** – When an LLM produces false or misleading information, often due to missing context or reaching context limits.
- **Tip:** Start a new chat for a new topic to keep context focused.

---

## 4. Retrieval-Augmented Generation (RAG)

- **RAG (Retrieval-Augmented Generation)** – A technique where external documents or data are retrieved, then passed to an LLM for generating better responses.
- **Retrieval** – The process of fetching relevant chunks of data based on a query.
- **Augmentation** – Adding retrieved data to the LLM’s input to provide context.
- **MCP (Model Context Protocol)** – A connector framework used to link LLMs with external data sources (APIs, files, databases).

---

## 5. Document Processing for RAG

- **Chunking** – Splitting large documents into smaller, manageable text segments.
- **Embedding** – Converting text chunks into numerical vector representations.
- **Vectorization** – The process of creating embeddings (vectors) for semantic search.
- **Vector Database (Vector DB)** – Specialized database that stores vectors for efficient similarity search.  
  Examples: **ChromaDB**, **Pinecone**, **Supabase**.

---

## 6. Semantic Search and Similarity

- **Semantic Search** – Finds information based on meaning rather than exact keyword matching.
- **Cosine Similarity** – A mathematical measure used to find which vectors (text chunks) are closest in meaning to the query.

---

## 7. Model Capabilities and Types

- **Text Generation Models** – LLMs designed to produce human-like text.
- **Image Generation Models** – AI models that generate images from text prompts.
- **Multimodal Models** – Models capable of processing and generating across multiple formats (text, image, audio).

---

## 8. Infrastructure and Runtime

- **GPU-Based Compute** – Graphics Processing Units are widely used for training and running LLMs due to their parallel processing power.
- **High-End CPU / Local Execution** – Smaller models (like 1.4 GB versions) can run locally on laptops for experimentation.

---

## 9. Best Practices

- Keep prompts focused and on-topic for accurate responses.
- Start a new chat or session when switching to a completely different topic.
- Use RAG when working with large knowledge bases to avoid exceeding context window limits.

---

## Key Takeaway

LLMs are the backbone of modern AI applications.  
Understanding tokens, context limits, embeddings, and RAG helps in building effective AI-powered solutions.
```


