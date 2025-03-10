# Medical Chatbot

A Flask-based application that uses RAG (Retrieval Augmented Generation) to answer medical questions by retrieving relevant information from medical PDFs.

## Overview

This project implements a conversational AI chatbot specialized in medical information using:
- LangChain framework for RAG implementation
- Flask for the web interface
- Pinecone as the vector database
- OpenAI for generating responses
- HuggingFace embeddings for text processing

The chatbot retrieves information from medical documents that have been processed, chunked, and stored in a Pinecone vector database to provide accurate and concise medical information.

## Features

- User-friendly chat interface
- Retrieval of relevant medical information from indexed PDFs
- Concise responses (limited to three sentences)
- Similarity-based document retrieval

## Prerequisites

- Python 3.7+
- Pinecone API key
- OpenAI API key

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/yasithS/Healthie-AI
   cd medical-chatbot
   ```

2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Create a `.env` file in the root directory with the following variables:
   ```
   PINECONE_API_KEY=your_pinecone_api_key
   OPENAI_API_KEY=your_openai_api_key
   ```

## Usage

### Data Preparation and Indexing

1. Place your medical PDF documents in a `Data/` directory in the project root.

2. Run the indexing script to process and store the documents in Pinecone:
   ```
   python store_index.py
   ```

### Running the Application

1. Start the Flask application:
   ```
   python app.py
   ```

2. Open a web browser and navigate to:
   ```
   http://localhost:8080
   ```

3. Interact with the chatbot by typing medical questions in the chat interface.

## Project Structure

```
medical-chatbot/
├── app.py                  # Main Flask application
├── Data/                   # Directory for medical PDF documents
├── Research/               # Directory contains notebooks               
├── setup.py                # Package setup file
├── requirements.txt        # Project dependencies
├── store_index.py          # Script to process and index documents
├── src/
│   ├── __init__.py
│   ├── helper.py           # Utilities for document loading and processing
│   └── prompt.py           # System prompt for the chatbot
├── static/
│   └── style.css           # CSS styles for the chat interface
└── templates/
    └── chat.html           # HTML template for the chat interface
```

## How It Works

1. **Document Processing**:
   - Medical PDFs are loaded and split into smaller chunks
   - Each chunk is embedded using HuggingFace's MiniLM model

2. **Information Retrieval**:
   - User queries are processed to find the most relevant document chunks
   - The system retrieves the top 3 most similar chunks using Pinecone

3. **Response Generation**:
   - Retrieved contexts are provided to OpenAI's model
   - Responses are generated following the system prompt guidelines (concise, three sentences maximum)

## Customization

- Modify the system prompt in `src/prompt.py` to change the chatbot's behavior
- Adjust the `chunk_size` and `chunk_overlap` in `src/helper.py` to optimize retrieval performance
- Change the `temperature` and `max_tokens` in `app.py` to control response length and creativity

## License

MIT License

## Acknowledgements

- Created by Yasith Gunawardhana
- gunawardhanayasith@gmail.com
