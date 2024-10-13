# Dash Application

This is a FastAPI and Dash application containerized using Docker and Docker Compose.

![Application Architecture](assets/ui.png)

## Prerequisites

- Docker: [Install Docker](https://docs.docker.com/get-docker/)
- Docker Compose: [Install Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

### 1. Clone the Repository (Branch ```ui```)

```sh
git clone -b ui git@gitlab.com:deep-learning4541742/mlapp.git
cd mlapp
```

### Create a requirements.txt File
List all the dependencies your application needs. For example:

```requirements.txt
dash
requests
numpy
base64
```

### Dockerfile
Create a Dockerfile in the root of your project:

```docker
# Use the official Python image from the Docker Hub
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container
COPY requirements.txt .

# Install the dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code into the container
COPY . .

# Expose the port the app runs on
EXPOSE 8000

# Command to run the Dash application
CMD ["python", "app.py"]

```


### Docker Compose
Create a docker-compose.yml file in the root of your project:

```docker compose
version: '3.8'

services:
  dash-app:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - .:/app
    environment:
      - PYTHONUNBUFFERED=1

```


### Build and Run the Docker Container
#### Using Docker Compose
To build and run the application using Docker Compose, run:

```Dockerfile
docker-compose up --build
```

### Using Docker Directly
To build and run the application using Docker directly, run:

```Dockerfile
docker build -t dash-app .
docker run -p 8000:8000 dash-app
```

### Access the Application
Once the container is running, you can access the Dash application at:

```
http://localhost:8000
```

