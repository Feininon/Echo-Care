
# Mental Health Chatbot

## Overview

This Flask application provides a mental health chatbot that offers emotional support, mindfulness tips, and
advice. It uses the following technologies:

*   **Flask:** A micro web framework for building the application.
*   **Flask-Bcrypt:** For secure password hashing.
*   **Flask-Login:** For user authentication and session management.
*   **PyMongo:**  For storing user data and chat history in a MongoDB database.
*   **Faiss:** For efficient similarity search and retrieval of relevant chat history using vector embeddings.
*   **Ollama:** For running and interacting with Large Language Models (LLMs) locally, specifically llama3.2 for
generating chatbot responses.
*   **Langchain-Ollama:** For embedding documents using Ollama models.

## Features

*   **User Authentication:** Secure user registration and login with password hashing.
*   **Chat Interface:**  Allows users to interact with the chatbot through a web interface.
*   **Chat History:** Stores and retrieves user chat history.
*   **Contextual Responses:**  Leverages Faiss and vector embeddings to retrieve relevant chat history and provide
more contextually aware responses.
*   **Crisis Detection:** Detects potential crisis situations (suicidal thoughts, self-harm) and provides helpful
resources.
*   **Emotional Support:** Provides compassionate and supportive responses to user messages.
*   **Local LLM:** Uses a local LLM (llama3.2) for generating responses, reducing reliance on external APIs.

## Prerequisites

*   **Python 3.7 or higher**
*   **MongoDB:**  A running MongoDB instance (local or remote).
*   **Ollama:**  Install Ollama and download the llama3.2 model: [https://ollama.com/](https://ollama.com/)
*   **Required Python Packages:**  Install the necessary packages using `pip`:

## Setup and Installation

1.  **Clone the Repository:**

```bash
git clone [repository_url]
cd [repository_directory]
```

2.  **Configure Environment Variables:**

    *   **MongoDB Connection String:** Ensure your MongoDB instance is running and configure the connection string
if necessary (defaults to `mongodb://localhost:27017/`). The application connects to `mongodb://localhost:27017/`
and uses the database "mental\_health\_chatbot".

3.  **Install Dependencies:**

```bash
pip install Flask Flask-Bcrypt Flask-Login pymongo faiss-cpu langchain-ollama ollama
```

4.  **Run the Application:**

```bash
python app.py
```

The application will start and be accessible in your web browser (usually at `http://127.0.0.1:5000/`).

## Directory Structure

```
mental_health_chatbot/
├── app.py          # Flask application file
├── README.md       # This file
├── faiss_indexes/   # Directory to store Faiss indexes (created at runtime)
├── messages/       # Directory to store message histories (created at runtime)
```

## Usage

1.  **Sign Up:**  Create an account by providing a username and password.
2.  **Log In:**  Log in with your credentials.
3.  **Chat:**  Start chatting with the chatbot.  Your chat history will be stored and used to provide more
relevant responses.

```mermaid
graph TD
    A[User] --> B{Flask App (app.py)};
    B --> C{Login/Signup};
    C -- Signup --> D[Store User Data in MongoDB];
    C -- Login --> E{Authentication with Bcrypt};
    E -- Success --> F[Load User FAISS Index & Message Store];
    E -- Failure --> C;
    F --> G[Chat Interface];
    G --> H{User Input};
    H --> I[Detect Crisis Keywords];
    I -- Crisis Detected --> J[Display Crisis Resources & Stop Chat];
    I -- No Crisis --> K[Retrieve Context from FAISS];
    K --> L[Generate Response with Ollama (llama3.2)];
    L --> M[Store User Input & Bot Response in MongoDB & FAISS];
    M --> G;
    G --> N{Logout};
    N --> O[End Session];
    D --> G;
    style A fill:#f9f,stroke:#333,stroke-width:2px
    style J fill:#fcc,stroke:#333,stroke-width:2px
```

## License

This project is licensed under the [MIT License](LICENSE).  See the `LICENSE` file for more information.

## Disclaimer

This chatbot is intended for informational and supportive purposes only and should not be considered a substitute
for professional mental health care.  If you are experiencing a mental health crisis, please reach out to a
qualified mental health professional or contact a crisis hotline.


