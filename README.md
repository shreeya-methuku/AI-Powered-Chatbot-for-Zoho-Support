# AI-Powered Chatbot for Zoho Support

This project is a sophisticated, AI-driven chatbot designed to streamline access to information about Zoho's suite of business applications. By leveraging a Retrieval-Augmented Generation (RAG) architecture, the chatbot provides accurate, context-aware answers to user queries by drawing directly from official Zoho documentation.

## Table of Contents

- [Project Objective](#project-objective)
- [Key Features](#key-features)
- [Architecture and Technologies](#architecture-and-technologies)
  - [Core Components](#core-components)
  - [Workflow](#workflow)
- [Technologies Used](#technologies-used)
- [Evaluation](#evaluation)
- [How to Use](#how-to-use)

## Project Objective

The primary goal of this project was to create an intelligent assistant that could simplify the process of finding information about Zoho applications like Zoho Books, Payroll, Inventory, and Analytics [file:11]. The chatbot was designed to understand natural language questions and provide reliable answers based on a comprehensive, pre-indexed knowledge base of Zoho's official documentation, thereby reducing the time and effort required to find operational and technical information [file:11].

## Key Features

-   **Multi-Product Support**: The chatbot is capable of answering questions related to various Zoho products, with the ability to switch between different knowledge bases [file:11].
-   **Dynamic Knowledge Base**: The system can crawl and index new Zoho documentation from provided URLs, allowing for an up-to-date and expandable knowledge base [file:11].
-   **Interactive Chart Generation**: Users can upload a CSV or Excel file and ask the chatbot to generate data visualizations using natural language commands (e.g., "Plot sales trend over time") [file:11].
-   **Dual-Model Support**: The chatbot can be configured to use either the OpenAI `gpt-3.5-turbo` model for high-quality responses or a local Hugging Face model (`Flan-T5`) for offline use [file:11].
-   **User-Friendly Web Interface**: A clean and responsive web interface, built with Gradio, allows for easy interaction, including product selection and file uploads [file:11].

## Architecture and Technologies

The chatbot is built on a Retrieval-Augmented Generation (RAG) architecture, which ensures that the answers provided are not only fluent and conversational but also grounded in factual information from the knowledge base.

### Core Components

1.  **Document Crawling and Indexing**:
    -   `Playwright` is used to dynamically crawl and extract content from Zoho's official documentation pages [file:11].
    -   `BeautifulSoup` and `readability-lxml` parse and clean the HTML to extract meaningful text [file:11].
    -   The extracted text is split into smaller, overlapping chunks for efficient processing [file:11].

2.  **Embedding and Vector Storage**:
    -   The `SentenceTransformers` library (`all-MiniLM-L6-v2` model) is used to convert the text chunks into dense vector embeddings [file:11].
    -   `FAISS` (Facebook AI Similarity Search) creates a highly efficient, searchable vector index from these embeddings [file:11].

3.  **Retrieval and Response Generation**:
    -   When a user submits a query, `FAISS` performs a semantic search to retrieve the most relevant text chunks from the indexed knowledge base [file:11].
    -   The retrieved context, along with the user's question, is passed to an OpenAI language model (`gpt-3.5-turbo`) [file:11].
    -   The model is instructed to generate an answer strictly based on the provided context, minimizing the risk of "hallucinations" or incorrect information [file:11].

### Workflow

1.  **User Query**: The user asks a question through the Gradio web interface.
2.  **Semantic Search**: The chatbot's backend uses FAISS to find the most relevant documents from its vector store.
3.  **Context Augmentation**: The retrieved documents are combined with the user's query to form a detailed prompt.
4.  **Answer Generation**: The prompt is sent to the OpenAI API, which generates a natural language response.
5.  **Display**: The final answer is displayed to the user in the chat interface.

## Technologies Used

-   **Programming Language**: Python [file:11]
-   **Core AI/ML Libraries**:
    -   `OpenAI API` for language model-based response generation [file:11].
    -   `SentenceTransformers` for creating text embeddings [file:11].
    -   `FAISS` for efficient similarity search [file:11].
    -   `Hugging Face Transformers` for local model support [file:11].
-   **Web Scraping & Parsing**:
    -   `Playwright` for dynamic web crawling [file:11].
    -   `BeautifulSoup` and `readability-lxml` for HTML parsing and text extraction [file:11].
-   **Web Interface**:
    -   `Gradio` for creating the interactive web application [file:11].
-   **Data Handling**:
    -   `Pandas` for handling uploaded data files (CSV/Excel) [file:11].
    -   `Matplotlib` for generating data visualizations [file:11].

## Evaluation

The chatbot was tested on a wide range of queries related to Zoho's functionalities, such as "How to enable GST in Zoho Books?" and "What are the supported payment gateways in Zoho Inventory?" [file:11].

The results were highly positive, with the chatbot demonstrating [file:11]:
-   **High Relevance**: The RAG architecture ensured that the answers were factually correct and directly related to the user's question.
-   **Fluency**: The use of a large language model resulted in responses that were natural and easy to understand.
-   **Robustness**: In cases where the knowledge base lacked sufficient information, the chatbot provided a clear fallback response, effectively avoiding the generation of incorrect information.

## How to Use

1.  **Clone the repository**:
    ```
    git clone <your-repository-url>
    ```
2.  **Install dependencies**:
    ```
    pip install pandas numpy openai sentence-transformers faiss-cpu gradio playwright beautifulsoup4 readability-lxml
    ```
3.  **Set up OpenAI API Key**: Make sure to set your OpenAI API key as an environment variable.
4.  **Run the application**:
    ```
    python app.py
    ```
5.  **Access the web interface**: Open your browser and navigate to the local URL provided by Gradio to start interacting with the chatbot.

