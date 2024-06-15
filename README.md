## API Reference

### Getting Started
- **Base URL**: At present, this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, `http://127.0.0.1:5000/`, which is set as a proxy in the frontend configuration.
- **Authentication**: This version of the application does not require authentication or API keys.

### Error Handling
Errors are returned as JSON objects in the following format:
```json
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```
### Endpoints
### GET /categories
- General:
    - Returns a list of all categories.
- Sample: curl http://127.0.0.1:5000/categories
```json
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  }
}
```
### GET /questions
- General:
  - Returns a list of questions, success value, total number of questions, current category, and categories.
  - Results are paginated in groups of 10. Include a request argument to choose page number, starting from 1.
- Sample: curl http://127.0.0.1:5000/questions?page=1
```json
{
  "questions": [
    {
      "id": 1,
      "question": "What is the largest planet in our solar system?",
      "answer": "Jupiter",
      "category": "1",
      "difficulty": 2
    },
    {
      "id": 2,
      "question": "What is the capital of France?",
      "answer": "Paris",
      "category": "3",
      "difficulty": 1
    }
  ],
  "total_questions": 20,
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "success": true
}
```

### DELETE /questions/{question_id}
- General:
  - Deletes the question of the given ID if it exists. Returns the ID of the deleted question, success value, total questions, and question list based on current page number to update the frontend.
- Sample: curl -X DELETE http://127.0.0.1:5000/questions/1
```json
{
  "success": true,
  "deleted": 1,
  "questions": [
    {
      "id": 2,
      "question": "What is the capital of France?",
      "answer": "Paris",
      "category": "3",
      "difficulty": 1
    }
  ],
  "total_questions": 19
}
```

### POST /questions
- General:
  - Creates a new question using the submitted question, answer, category, and difficulty. Returns the ID of the created question, success value, total questions, and question list based on current page number to update the frontend.
- Sample: curl -X POST http://127.0.0.1:5000/questions -H "Content-Type: application/json" -d '{"question":"Who wrote '1984'?","answer":"George Orwell","category":"2","difficulty":2}'
```json
{
  "success": true,
  "created": 25,
  "questions": [
    {
      "id": 1,
      "question": "What is the largest planet in our solar system?",
      "answer": "Jupiter",
      "category": "1",
      "difficulty": 2
    },
    {
      "id": 2,
      "question": "What is the capital of France?",
      "answer": "Paris",
      "category": "3",
      "difficulty": 1
    }
  ],
  "total_questions": 21
}
```

### POST /questions/search
- General:
  - Searches for questions using a search term. Returns any questions for whom the search term is a substring of the question.
- Sample: curl -X POST http://127.0.0.1:5000/questions/search -H "Content-Type: application/json" -d '{"searchTerm":"capital"}'
```json
{
  "success": true,
  "questions": [
    {
      "id": 2,
      "question": "What is the capital of France?",
      "answer": "Paris",
      "category": "3",
      "difficulty": 1
    }
  ],
  "total_questions": 1
}
```

### GET /categories/{category_id}/questions
- General:
  - Returns a list of questions for a specific category, success value, and total number of questions.
- Sample: curl http://127.0.0.1:5000/categories/1/questions
```json
{
  "success": true,
  "questions": [
    {
      "id": 1,
      "question": "What is the largest planet in our solar system?",
      "answer": "Jupiter",
      "category": "1",
      "difficulty": 2
    }
  ],
  "total_questions": 1
}
```

### POST /quizzes
- General:
    - Returns a random question to play the quiz, given a category and not in a list of previous questions.
- Sample: curl -X POST http://127.0.0.1:5000/quizzes -H "Content-Type: application/json" -d '{"quiz_category":{"type":"Science","id":"1"},"previous_questions":[1, 4, 20]}'
```json
{
  "success": true,
  "question": {
    "id": 5,
    "question": "What is the chemical symbol for the element oxygen?",
    "answer": "O",
    "category": "1",
    "difficulty": 1
  }
}

```