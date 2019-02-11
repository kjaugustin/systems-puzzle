# Insight DevOps Engineering Systems Puzzle Solution

## Table of Contents

1. [Introduction](README.md#introduction)
2. [Puzzle details](README.md#puzzle-details)
3. [Steps to solve the puzzle](README.md#Steps-to-solve-the-puzzle)




# Introduction

Imagine you're on an engineering team that is building an eCommerce site where users can buy and sell items (similar to Etsy or eBay). One of the developers on your team has put together a very simple prototype for a system that writes and reads to a database. The developer is using Postgres for the backend database, the Python Flask framework as an application server, and nginx as a web server. All of this is developed with the Docker Engine, and put together with Docker Compose.

Unfortunately, the developer is new to many of these tools, and is having a number of issues. The developer needs your help debugging the system and getting it to work properly.

# Puzzle details

The codebase included in this repo is nearly functional, but has a few bugs that are preventing it from working properly. The goal of this puzzle is to find these bugs and fix them. 

Assuming you have the Docker Engine and Docker Compose already installed, the developer said that the steps for running the system is to open a terminal, `cd` into this repo, and then enter these two commands:

    docker-compose up -d db
    docker-compose run --rm flaskapp /bin/bash -c "cd /opt/services/flaskapp/src && python -c  'import database; database.init_db()'"

This "bootstraps" the PostgreSQL database with the correct tables. After that you can run the whole system with:

    docker-compose up -d

At that point, the web application should be visible by going to `localhost:8080` in a web browser. 



# Steps to solve the puzzle
* Changed nginx port settings to '8080:80' in docker-compose.yml
* Added flask port settings in docker-compose.yml. Used the default settings of 5000:5000
* flaskapp port 5000 exposed in Dockerfile
* flaskapp.conf has been corrected to reflect the correct port number of 5000. 
    proxy_pass http://flaskapp:5000
* Modified the app.py(success route) to show all items added to the database. 
* Modified app.py to enable runtime debugging.

    app.run(host='0.0.0.0', debug=True)


