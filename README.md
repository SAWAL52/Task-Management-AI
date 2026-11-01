# Task Management AI

Task Management AI is a conversational task management application built using Python, Streamlit, LangChain, Groq, LangGraph, and SQLite.

The application uses a Groq-hosted large language model to interpret natural language instructions and interact with an SQLite database through LangChain's SQL Database Toolkit. Users can create, view, update, and delete tasks through a chat interface without writing SQL queries manually.

## Features

- **LLM Integration with Groq:** Uses the `openai/gpt-oss-120b` model for understanding user instructions and generating responses.
- **Agent Creation with LangChain:** Uses `create_agent` to build an AI agent capable of interacting with database tools.
- **SQL Database Integration:** Connects to an SQLite database using LangChain's `SQLDatabase` utility.
- **SQL Database Toolkit:** Uses `SQLDatabaseToolkit` to provide the agent with tools for inspecting and interacting with the database.
- **Task Management (CRUD):** Supports creating, retrieving, updating, and deleting tasks through natural language.
- **Conversational Memory:** Uses LangGraph's `InMemorySaver` to maintain conversation context across interactions.
- **Real-Time Response Streaming:** Displays generated responses incrementally using LangChain and Streamlit.
- **Interactive Chat Interface:** Provides a conversational interface built with Streamlit.
- **Session State Management:** Uses Streamlit session state to maintain chat history and conversation thread IDs.
- **Task Status Management:** Supports three task statuses: `pending`, `in_progress`, and `completed`.
- **Chat Management:** Includes a Clear Chat feature to reset the current conversation.
- **Environment Variable Management:** Uses `python-dotenv` to load the Groq API key securely.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Streamlit | User interface and session management |
| LangChain | Agent creation and orchestration |
| LangChain Groq | Groq model integration |
| LangChain Community | SQL database integration and toolkit |
| LangGraph | Conversational memory and checkpointing |
| Groq | Large language model inference |
| SQLite | Task data storage |
| python-dotenv | Environment variable management |

## Requirements

- Python 3.10 or later
- Groq API key
- Internet connection

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/SAWAL52/Task-Management-AI.git
cd Task-Management-AI
```

### 2. Create and activate a virtual environment

For macOS and Linux:

```bash
python3 -m venv env
source env/bin/activate
```

For Windows:

```bash
python -m venv env
env\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Create a `.env` file in the root directory:

```env
GROQ_API_KEY=your_groq_api_key
```

Obtain your API key from the [Groq Console](https://console.groq.com/).

### 5. Run the application

```bash
streamlit run app.py
```

The application will be available at:

`http://localhost:8501`

## How It Works

1. The user enters a task-related instruction through the Streamlit chat interface.
2. Streamlit session state manages the conversation history and thread ID.
3. The request is passed to the LangChain agent.
4. The Groq-hosted language model interprets the user's instruction.
5. The agent selects the appropriate SQL database tool from the SQLDatabaseToolkit.
6. The selected tool performs the required database operation on the SQLite database.
7. After a create, update, or delete operation, the agent is instructed to retrieve the updated task information.
8. LangGraph's InMemorySaver maintains conversation context using the thread ID.
9. The generated response is streamed to the Streamlit interface.

## Database Structure

The application uses an SQLite database named `my_tasks.db`.

### Tasks Table

| Column | Data Type | Description |
|---|---|---|
| id | INTEGER | Primary key and auto-incrementing task ID |
| title | TEXT | Task title |
| description | TEXT | Task description |
| status | TEXT | Task status |
| created_at | TIMESTAMP | Task creation timestamp |

### Available Task Statuses

- `pending`
- `in_progress`
- `completed`

The database and tasks table are created automatically when the application initializes.

## Project Structure

```text
Task-Management-AI/
├── app.py
├── README.md
├── requirements.txt
├── .env.example
└── .gitignore
```

The `my_tasks.db` file is generated locally when the application runs and is excluded from version control.

## Limitations

- An active internet connection is required for Groq API access.
- A valid Groq API key is required.
- The application uses SQLite for local database storage.
- Database records are stored locally and are not synchronized between separate installations.
- LangGraph's in-memory checkpointing does not preserve conversation memory after the application process restarts.
- AI-generated SQL operations and responses may not always be accurate.
- The application is intended for local development and learning purposes, not production use without additional security controls.

## Future Improvements

- Add task priority and due-date management.
- Introduce task search and filtering.
- Display tasks in a dedicated dashboard.
- Add task completion statistics.
- Implement persistent conversation memory.
- Add user authentication and individual task management.
- Improve database operation validation and error handling.
- Add task editing and deletion controls through the interface.

## License

This project is intended for learning and development purposes.