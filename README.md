# Casting Agency API Backend



## About

The Casting Agency API is used to store details of actors and movies. 
The API allows:
- The Casting Assistant to view actors and movies.
- The Executive Producer to view, post, update and delete actors and movies.

All endpoints need to be tested using curl or postman since there is no frontend for the app.

#### Motivation
I have developed this api with the help of the courses that I have followed in the Udacity fullstack nanodegree. It has helped me to put in practice and consolidate the various elements taught during the nanodegree. And it seems to be running well, which is great.



## Getting Started

### Installing Dependencies

#### Python 3.9
Follow the instructions to install the latest version of Python for your platform in the python website (https://docs.python.org/).

#### PIP Dependencies
In the FSND_Capstone2 directory, run the following to install all necessary dependencies:
- Install virtual env:
'''
$ pip3 install virtualenv
$ python3 -m virtualenv venv
$ source venv/bin/activate
'''
- Install dependencies:
'''
pip3 install -r requirements.txt
'''

#### Key Dependencies
- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in api.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

#### Prepare the Database 
- Create Postgres database:
'''
$ createdb new_database_name
'''
- Update database name 'database_name' in models.py



## RUNNING THE APP
In the FSND_Capstone2 directory, run the following:
'''
$ export FLASK_APP=src.api.py
$ export FLASK_ENV=development
$ flask run
'''

The API endpoints can also be accessed via Heroku using the URL:
https://fsnd-capstone2-heroku-app.herokuapp.com



## DEPLOY THE APP VIA HEROKU
In order to deploy the API on Heroku, navigate to the 'FSND_Capstone2' folder and run the following commands:
- Login Heroku:
'''
$ heroku login
'''
- Create the Heroku app:
'''
$ heroku create fsnd-capstone2-heroku-app
'''
- Create an Heroku database:
'''
$ heroku addons:create heroku-postgresql:hobby-dev
'''
- Deploy the app:
$ git add .
$ git commit -m 'comment'
$ git push heroku master
'''



## DATA MODELLING
### models.py
The schema for the database and helper methods to simplify API behaviour are in models.py:
- There are two tables created: Actors and Movies
- The Actors table is used for the actor details: name, age and gender.
- The Movie table is used for the movie details: title and release date.
Each table has an inser, update, delete and patch helper function.



## ARCHITECTURE AND TESTING
### Endpoint Library
@app.errorhandler decorators were used to format error responses as JSON objects. 
Custom @requires_auth decorators were used for Authorization based on roles of the user. Two roles are assigned to the API: 'CastingAssistant' and 'ExecutiveProducer'.

The JWT for the Casting Assistant: see setup.sh
The JWT for the Executive Producer: see setup.sh

#### GET /actors
- General:
    - Returns a list of actors names, age and gender, and a success value.

'''
[
    {
        "actors": [
            {
                "age": 55,
                "gender": "Male",
                "id": 1,
                "name": "Eddie Dean"
            },
            {
                "age": 35,
                "gender": "Male",
                "id": 2,
                "name": "Tim Pum"
            },
            {
                "age": 45,
                "gender": "Female",
                "id": 3,
                "name": "Ella Shu"
            },
            {
                "age": 30,
                "gender": "Female",
                "id": 4,
                "name": "Dina Gove"
            },
            {
                "age": 20,
                "gender": "Female",
                "id": 5,
                "name": "Ola Titi"
            }
        ],
        "success": true
    },
    200
]
'''

#### GET /movies
- General:
    - Returns the list of movies (title and release date) and a success value.

'''
[
    {
        "movies": [
            {
                "id": 1,
                "release_date": "Sun, 29 Oct 2000 00:00:00 GMT",
                "title": "James Bond 1"
            },
            {
                "id": 2,
                "release_date": "Wed, 03 Mar 2004 00:00:00 GMT",
                "title": "James Bond 2"
            },
            {
                "id": 3,
                "release_date": "Fri, 06 Jun 2008 00:00:00 GMT",
                "title": "James Bond 3"
            },
            {
                "id": 4,
                "release_date": "Sun, 01 Feb 1970 23:00:00 GMT",
                "title": "Alice in Wonderland"
            },
            {
                "id": 5,
                "release_date": "Fri, 02 Feb 2018 00:00:00 GMT",
                "title": "Upsy Daisy"
            }
        ],
        "success": true
    },
    200
]
'''

#### DELETE /actors/(actor_id)
- General:
    - Delete the actor with the id 'actor_id' if it exists. Returns a deleted value, the id of the deleted actor and a success value.

'''
[
    {
        "actor": {
            "age": 30,
            "gender": "Female",
            "id": 4,
            "name": "Dina Gove"
        },
        "success": true
    },
    200
]
'''

#### DELETE /movies/(movie_id)
- General:
    - Delete the movie with the id 'movie_id' if it exists. Returns a deleted value, the id of the deleted movie and a success value.

'''
[
    {
        "movie": {
            "id": 4,
            "release_date": "Sun, 01 Feb 1970 23:00:00 GMT",
            "title": "Alice in Wonderland"
        },
        "success": true
    },
    200
]
'''

#### POST /actors
- General:
    - Creates a new actor (name, age and gender). 
    Returns a created value, the id of the created actor and a success value.

'''
[
    {
        "actor": {
            "age": 70,
            "gender": "Male",
            "id": 6,
            "name": "Didier Nala"
        },
        "success": true
    },
    200
]
'''

#### POST /movies
- General:
    - Creates a new movie (title and release_date). 
    Returns a created value, the id of the created movie and a success value.

'''
[
    {
        "movie": {
            "id": 6,
            "release_date": "Mon, 07 Jul 1980 00:00:00 GMT",
            "title": "Happy Ferry"
        },
        "success": true
    },
    200
]
'''

#### PATCH /actors/(actor_id)
- General:
    - Updates the actor with the id 'actor_id' if it exists (name, age and gender). 
    Returns a created value, the id of the updated actor and a success value.

'''[
    {
        "actor": {
            "age": 99,
            "gender": "Female",
            "id": 2,
            "name": "Filipa"
        },
        "success": true
    },
    200
]
'''

#### PATCH /movies/(movie_id)
- General:
    - Updates the movie with the id 'movie_id' if it exists (title and release_date). 
    Returns a created value, the id of the updated movie and a success value.

'''
[
    {
        "movie": {
            "id": 2,
            "release_date": "Wed, 01 Jan 2003 00:00:00 GMT",
            "title": "James Bond 2"
        },
        "success": true
    },
    200
]
'''

#### Error Handling
Errors are returned as JSON objects in the following format:
'''
{
    "success": False,
    "error": 400,
    "message": "bad request"
}

The API will return three error types when requests fail:
- 400: bad request
- 404: resource not found
- 405: method not allowed
- 422: unprocessable



## TESTING
In order to run tests locally (unittests), 
- Duplicate the Postgres database:
'''
$ psql database_name
psql> \l
psql> CREATE DATABASE database_name_for_tests WITH TEMPLATE database_name;
'''
- Update database name 'database_name' in test_api.py
- Navigate to the 'FSND_Capstone2' folder and run the following commands:
'''
$ python3 -m src.test_api
'''



## THIRD-PARTY AUTHENTICATION
### auth.py
Auth0 is set up and running. The following configurations are in the setup.sh file:
- The Auth0 domain name
- The Auth0 Alogorithm
- The Auth0 API audience
- The Database URL
The JWTs are also provided in the setup.sh file.



## DEPLOYMENT
The app is hosted live on Heroku at the URL:
https://fsnd-capstone2-heroku-app.herokuapp.com

However note that there is no frontend for this app.



# Authors
Vincent Moutel, with lots of help and parts copied from the Udacity Full-stack Nanodegree.



# Acknowledgements
Udacity and everybody on the Udacity forum
