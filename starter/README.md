# Backend - Full Stack Trivia API 

### Installing Dependencies for the Backend

1. **Python 3.7** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)


2. **Virtual Enviornment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)


3. **PIP Dependencies** - Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:
```bash
pip install -r requirements.txt
```
This will install all of the required packages we selected within the `requirements.txt` file.


4. **Key Dependencies**
 - [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

 - [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

 - [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

### Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

### Running the server

From within the `./src` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

# Backend - Full Stack Trivia API END POINTS

## Getting Started
- Base URL: At present, the API is in a very early stage of development. It only runs on localhost and is not yet ready for production use.
   The backend app is currenlty hosted on `http://127.0.0.1:5000/`.
- Authentication: The API is currently not protected. Anyone can access it.

## Error Handling
- The API returns a JSON object with the following fields:
   - `success`: Boolean indicating whether the request was successful.
   - `error`: Integer containing the error code.
   - `message`: resources could not be found.
 `{
    "success": False, 
    "error": 400,
    "message": "bad request"
}`
- The error codes are as follows:
   - 400: Bad request.
   - 401: Unauthorized.
   - 404: Not found.
   - 422: Unprocessable.

## Endpoints

### GET /catetories
- Returns a list of all categories.
- Response:
    `{
        "success": True,
        "categories": [
            {
                "id": 1,
                "type": "Category 1"
            },
            {
                "id": 2,
                "type": "Category 2"
            }
        ]
    }`

### GET /questions
- General
    - Returns a list of a list of questions, number of total questions, current category, categories.  
    - Results are paginated in groups of 10. Include a reuqest argument `page` to specify the page number, start from 1.
    - Example: `http://127.0.0.1:5000/questions?page=1`
- Sample result:

   `{"categories":{"1":"Science","2":"Art","3":"Geography","4":"History","5":"Entertainment","6":"Sports"},"current_category":{"id":1,"type":"Science"},"questions":[{"answer":"Apollo 13","category":5,"difficulty":4,"id":2,"question":"What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"},{"answer":"Tom Cruise","category":5,"difficulty":4,"id":4,"question":"What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"},{"answer":"Maya Angelou","category":4,"difficulty":2,"id":5,"question":"Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"},{"answer":"Edward Scissorhands","category":5,"difficulty":3,"id":6,"question":"What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"},{"answer":"Muhammad Ali","category":4,"difficulty":1,"id":9,"question":"What boxer's original name is Cassius Clay?"},{"answer":"Brazil","category":6,"difficulty":3,"id":10,"question":"Which is the only team to play in every soccer World Cup tournament?"},{"answer":"Uruguay","category":6,"difficulty":4,"id":11,"question":"Which country won the first ever soccer World Cup in 1930?"},{"answer":"George Washington Carver","category":4,"difficulty":2,"id":12,"question":"Who invented Peanut Butter?"},{"answer":"Lake Victoria","category":3,"difficulty":2,"id":13,"question":"What is the largest lake in Africa?"},{"answer":"The Palace of Versailles","category":3,"difficulty":3,"id":14,"question":"In which royal palace would you find the Hall of Mirrors?"}],"success":true,"total_questions":19}`

### POST /questions
- General:
    - Creates a new question using the submitted question, answer, category and difficulty. Returns the id of the created question , success value.
    - `curl http://127.0.0.1:5000/questions -X POST -H "Content-Type: application/json" -d '{"question":"sample question", "answer":"sample answer","category":"Science", "difficulty":"1"}'`
- Sample result:

    `{
        "success": True,
        "created": 1
    }`

### DELETE /questions/{question_id}
- General:
    - Deletes the question of the given ID if it exists. Returns the id of the deleted question, success value.
    - `curl -X DELETE http://127.0.0.1:5000/questions/1`
- Sample result:

  `{
    "success": true,
    "deleted": 1
  }`

### POST /questions/search
- General:
    - Searches for questions based on a given search term. Returns a list of questions and success value.
    - `curl -X POST http://127.0.0.1:5000/questions/search -H "Content-Type: application/json" -d '{"searchTerm":"sample"}'`
- Sample result:
  
    `{
        "success": True,
        "questions": [
            {
                "answer": "sample answer",
                "category": "Science",
                "difficulty": 1,
                "id": 1,
                "question": "sample question"
            }
        ],
        "total_questions": 1
        "current_category": null
    }`
### GET /categories/{category_id}/questions
- General:
    - Returns a list of questions for the given category.
    - `curl http://127.0.0.1:5000/categories/1/questions`
- Sample result:
  
    `{
        "success": True,
        "questions": [
            {
                "answer": "sample answer",
                "category": "Science",
                "difficulty": 1,
                "id": 1,
                "question": "sample question"
            }
        ],
        "total_questions": 1
        "current_category": 1
    }`
### POST /quizzes
- General:
    - Starts a new quiz with a given category. Returns a list of questions, success value.
    - `curl -X POST http://127.0.0.1:5000/quizze -H "Content-Type: application/json" -d '{"previous_questions":[],"quiz_category":{"type":"Science","id":1}}'`
- Sample result:

    `{
        "success": True,
        "question": {
            "answer": "sample answer",
            "category": "Science",
            "difficulty": 1,
            "id": 1,
            "question": "sample question"
        }
    }`

## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
