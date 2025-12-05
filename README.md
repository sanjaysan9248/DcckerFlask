# Flask App Docker Deployment on AWS EC2

This is a small project where I created a simple Flask application, put it inside a Docker container, and deployed it on an AWS EC2 Ubuntu instance.  
The main purpose of this project was to understand how Docker works, how to run containers on a cloud server, and how to expose the app publicly.

---

## What this project contains
- A basic Flask app (`sanapp.py`)
- A `requirements.txt` file for dependencies
- A Dockerfile to build the Docker image
- Instructions to run the project locally or on AWS EC2

---

## Flask App (sanapp.py)

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Sanjay's Flask App!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

This is just a simple route that prints a message so I can test the deployment.

---

## Requirements

```
flask
```

---

## Dockerfile

```dockerfile
FROM python:3.9

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python3", "sanapp.py"]
```

---

## How to run this with Docker (locally or on EC2)

### Build the image:
```
docker build -t san-flask-app .
```

### Run the container:
```
docker run -d -p 5000:5000 san-flask-app
```

### Check if container is running:
```
docker ps
```

---

## Deploying on AWS EC2

### 1. Launch an Ubuntu EC2 instance
- Instance type: t2.micro or t3.micro  
- Open port **22** (SSH) and **5000** (for Flask)
- Download your `.pem` key

### 2. Connect to EC2
```
chmod 400 yourkey.pem
ssh -i yourkey.pem ubuntu@<EC2-IP>
```

### 3. Install Docker on EC2
```
sudo apt update
sudo apt install docker.io -y
```

### 4. Clone this repository
```
git clone https://github.com/sanjaysan9248/DcckerFlask.git
cd DcckerFlask
```

### 5. Build and run the Docker container on EC2
```
docker build -t san-flask-app .
docker run -d -p 5000:5000 san-flask-app
```

---

## Accessing the app
Open your browser and go to:

```
http://<EC2-IP>:5000
```

You should see:
```
Hello from Sanjay's Flask App!
```

---

## What I learned from this project
- How to write a simple Flask application  
- How Docker builds images and runs containers  
- How to connect to AWS EC2 with SSH  
- How port mapping works (5000 inside → 5000 outside)  
- How to deploy a containerized app on a cloud server  

---

## Future improvements
- Add Nginx reverse proxy  
- Use GitHub Actions (CI/CD)  
- Deploy using ECS or Kubernetes  
- Add logging and monitoring  

---

## Author
Sanjay  
