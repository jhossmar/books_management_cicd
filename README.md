# Developing a Single Page App with Flask and Vue.js

### Want to learn how to build this?

Check out the [post](https://testdriven.io/developing-a-single-page-app-with-flask-and-vuejs).

## Want to use this project?

1. Fork/Clone

1. Run the server-side Flask app in one terminal window:

    ```sh
    $ cd server
    $ python3.9 -m venv env
    $ source env/bin/activate
    (env)$ pip install -r requirements.txt
    (env)$ python app.py
    ```

    Navigate to [http://localhost:5000](http://localhost:5000)

1. Run the client-side Vue app in a different terminal window:

    ```sh
    $ cd client
    $ npm install
    $ npm run serve
    ```

    Navigate to [http://localhost:8080](http://localhost:8080)


##Bring up the services using docker:
  ### Build docker image 
  #### Before building, change the IP address where the Backend  service is running (client/src/components/Books.vue)
    ```$ cd server
   $ docker build -t backend:1.0 .
    ```
  
  #### Build frontend docker image
    ```$ cd client
   $ docker build -t frontend:1.0 .
    ```
   
  #### into the main folder start the services using docker-compose
    ```$ docker-compose up -d
     ```
