# Coffee Shop Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Environment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virtual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) and [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) are libraries to handle the lightweight sqlite database. Since we want you to focus on auth, we handle the heavy lift for you in `./src/database/models.py`. We recommend skimming this code first so you know how to interface with the Drink model.

- [jose](https://python-jose.readthedocs.io/en/latest/) JavaScript Object Signing and Encryption for JWTs. Useful for encoding, decoding, and verifying JWTS.

## Running the server

From within the `./src` directory first ensure you are working using your created virtual environment.

Each time you open a new terminal session, run:

```bash
export FLASK_APP=api.py;
export FLASK_ENV=development
```

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## Tasks

### Setup Auth0

1. Create a new Auth0 Account
2. Select a unique tenant domain
3. Create a new, single page web application
4. Create a new API
   - in API Settings:
     - Enable RBAC
     - Enable Add Permissions in the Access Token
5. Create new API permissions:
   - `get:drinks`
   - `get:drinks-detail`
   - `post:drinks`
   - `patch:drinks`
   - `delete:drinks`
6. Create new roles for:
   - Barista
     - can `get:drinks-detail`
     - can `get:drinks`
   - Manager
     - can perform all actions
7. Test your endpoints with [Postman](https://getpostman.com).
   - Register 2 users - assign the Barista role to one and Manager role to the other.
   - Sign into each account and make note of the JWT.
   - Import the postman collection `./starter_code/backend/udacity-fsnd-udaspicelatte.postman_collection.json`
   - Right-clicking the collection folder for barista and manager, navigate to the authorization tab, and including the JWT in the token field (you should have noted these JWTs).
   - Run the collection and correct any errors.
   - Export the collection overwriting the one we've included so that we have your proper JWTs during review!

### Implement The Server

There are `@TODO` comments throughout the `./backend/src`. We recommend tackling the files in order and from top to bottom:

1. `./src/auth/auth.py`
2. `./src/api.py`

http://localhost:8080/login-results#access_token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6ImotUTZQdlNmRnJmZUh6VGNMOUJ5ZSJ9.eyJpc3MiOiJodHRwczovL21hcnlibmdvemkudXMuYXV0aDAuY29tLyIsInN1YiI6ImF1dGgwfDYyYjBmM2U4ZjMzZjZkOTc0NjA3NGZmNiIsImF1ZCI6ImltYWdlIiwiaWF0IjoxNjU1NzY0MzEyLCJleHAiOjE2NTU3NzE1MTIsImF6cCI6Ik1lWmU1emJrQ09xcGtRSzVuNjVtZmVSQm1EcDgzNVRMIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJnZXQ6ZHJpbmtzIiwiZ2V0OmRyaW5rcy1kZXRhaWwiXX0.Ma32BLuq61EjaCS8BB95psIWUGG5XbWL3O1LHrJTbeMC5KPN9gUfTfJKMpNxUfD4NsNbbGtE0MyujoH8SVEuAX4Fla7dJR6DAjxR8tTkAmbbyXpt5dckZ5hkqCz6DAR48-vZEcc3HvIPqAAvq-UEtwy_3aC5IZIrhJABCfLlJfuqhMtOK7enWI_UW376hAuUIQ7aHnp9m0_0yfKuOgAkIH6-MCd1KTRV4wMX4OixxbfVUwaXuqLBk68YSeW0Y-oRrpE75a0aAu0IfpmHb3lFbV4f5gHvVH52ujmoht81SSVuFmkhHGWMg8KvfV6PoMdA8ulo6WIMdTwHs2icxczJhA&expires_in=7200&token_type=Bearer

http://localhost:8080/login-results#access_token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6ImotUTZQdlNmRnJmZUh6VGNMOUJ5ZSJ9.eyJpc3MiOiJodHRwczovL21hcnlibmdvemkudXMuYXV0aDAuY29tLyIsInN1YiI6ImF1dGgwfDYyYTk3YjY2NTcxMjBjODMwZmQxNDQ4OSIsImF1ZCI6ImltYWdlIiwiaWF0IjoxNjU1NzY0NzUzLCJleHAiOjE2NTU3NzE5NTMsImF6cCI6Ik1lWmU1emJrQ09xcGtRSzVuNjVtZmVSQm1EcDgzNVRMIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJkZWxldGU6ZHJpbmtzIiwiZ2V0OmRyaW5rcyIsImdldDpkcmlua3MtZGV0YWlsIiwicGF0Y2g6ZHJpbmtzIiwicG9zdDpkcmlua3MiXX0.Ka2cU45pI8JaJ4pOrcFYVtDZmhpHie25XOuB7uIjoiNAiuFEK6r_9JY_jfK_NVtLZkYhKWj3knc7vyW45LuaeqH3FwL6ywfJCgOgpzNOvyqRGwCAwH5Cd-q2f6ebfk5fy7qCFmGBam1qDszdN7In_30-w6-ykvau8dF75aHrQRMYi3uQm9pkveQbo4T9Gsts8wUmJoC4anuYBI9Fbqvq4gtxqjCqaGxiLccw-2AP2FOAg4zGtCnwV88mpftY65JTOYjkIN-n630a1N8Hd_U1Ug5f_YbORfWeVjoCi7RhMS_vJs5h55oQP3CTrLGXxqn23OeOLL43bp_3QRqosZuS1A&expires_in=7200&token_type=Bearer
