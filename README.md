# Chatbot Application with Flask and Groq API

This is a chatbot application built with Flask that interacts with a PostgreSQL database and utilizes the Groq API for AI-based completions. The chatbot answers user questions based on a set of pre-stored question-answer embeddings, categorizes questions into predefined clusters, and tracks user interaction. Additionally, it generates data visualizations to display the user's activity.

## Features

- **User Authentication**: Users can log in with their email address.
- **Real-time Chat**: Users can ask questions, and the chatbot will generate responses based on embeddings stored in the database.
- **User Activity Tracking**: The app tracks the number of questions asked by a user in various categories (clusters).
- **Graphical Representation of User Activity**: Generates bar charts to visualize the user's activity across different question categories.
- **Feedback Mechanism**: Users can provide feedback on chatbot responses, which is stored in the database.
- **Rate Limiting**: The application limits the number of questions a user can ask within a specified time frame to prevent abuse.

## Technologies Used

- **Flask**: Web framework for building the application.
- **Groq API**: AI-powered language model for generating chatbot responses.
- **PostgreSQL**: Database for storing question-answer embeddings, user data, and feedback.
- **Sentence-Transformers**: Model for generating sentence embeddings for queries.
- **Matplotlib**: Used for generating graphs based on user activity.
- **Seaborn**: Library for visualizing user activity data in a beautiful format.

## Requirements

To run this application locally, you'll need to have the following installed:

- Python 3.7+
- pip (Python package manager)
- PostgreSQL
- Groq API access (requires an API key)

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/chatbot-flask.git
cd chatbot-flask
2. Install Required Libraries
bash
Copy
Edit
pip install -r requirements.txt
3. Set Up PostgreSQL Database
Create a PostgreSQL database named su_bot_data.
Create the necessary tables by running the following SQL queries:
sql
Copy
Edit
CREATE TABLE IF NOT EXISTS qa_embeddings (
    question TEXT,
    answer TEXT,
    embedding VECTOR
);

CREATE TABLE IF NOT EXISTS user_data (
    mail_id TEXT,
    question_asked TEXT,
    cluster INTEGER
);

CREATE TABLE IF NOT EXISTS feedback (
    question TEXT,
    chatbot_response TEXT,
    user_rating INTEGER,
    user_feedback TEXT,
    flagged_for_review BOOLEAN
);
4. Configure Groq API
Sign up for Groq and get your API key. Add the key to the application by replacing the placeholder in the code:

python
Copy
Edit
client = Client(api_key="your-groq-api-key")
5. Run the Application
bash
Copy
Edit
python app.py
This will start the Flask application locally on port 5000. You can access it via http://127.0.0.1:5000/.

Endpoints
/ (GET)
Renders the login page.
/home (POST)
Accepts the user's email address and stores it in the session.
Clears the chat history.
/ask (POST)
Accepts the user's question and attempts to generate an answer based on stored embeddings and Groq's API.
Tracks user interaction and applies rate-limiting.
/submit_feedback (POST)
Allows users to provide feedback on the chatbot's response.
Stores the feedback in the database, with a flag if the rating is below 3.
/user_status (GET)
Displays a page where the user can view their interaction status.
/user_status_graph (POST)
Accepts a user ID (email address) and generates a bar chart visualizing the user's activity across different question clusters.
Rate Limiting
The application enforces a limit on the number of questions a user can ask within a one-hour period. The maximum allowed is 10 questions. If the limit is exceeded, the user is informed about the wait time until they can ask again.

Feedback
Users can rate the chatbot's response with a rating between 1 and 5. If the rating is less than 3, the feedback is flagged for review. This feedback is stored in the feedback table in PostgreSQL.

Graphical User Interface (GUI)
The interface consists of a login page, a chat interface where users can ask questions, and a feedback form.
Users can also view their activity graph, which visualizes the number of questions asked in different categories.
License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgements
Groq API: For providing the AI-powered chatbot completion model.
Sentence-Transformers: For the sentence embeddings used in the question-answer matching.
PostgreSQL: For data storage.
Flask: For building the web application.
Contributions
Contributions are welcome! Feel free to open issues and submit pull requests.
