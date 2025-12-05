# Flask App Deployment using Docker and AWS EC2

This is a small learning project where I ran a simple Flask application inside a Docker container and deployed it on an AWS EC2 Ubuntu instance.  
I did this to understand Docker basics and how deployment works on the cloud.

## Files in this project
- sanapp.py → Flask app  
- requirements.txt → dependencies  
- Dockerfile → used to build the Docker image  

## Flask App Code

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Sanjay's Flask App!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

## requirements.txt

```
flask
```

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

## Running it with Docker

### Build the image:
```
docker build -t san-flask-app .
```

### Run the container:
```
docker run -d -p 5000:5000 san-flask-app
```

### Check containers:
```
docker ps
```

## Steps I followed on AWS EC2

1. Launched Ubuntu EC2 instance  
2. Opened ports 22 (SSH) and 5000  
3. Connected with SSH:
```
chmod 400 mykey.pem
ssh -i mykey.pem ubuntu@<EC2-IP>
```
4. Installed Docker:
```
sudo apt update
sudo apt install docker.io -y
```
5. Cloned the repo:
```
git clone https://github.com/sanjaysan9248/DcckerFlask.git
cd DcckerFlask
```
6. Built and ran the Docker container:
```
docker build -t san-flask-app .
docker run -d -p 5000:5000 san-flask-app
```

## How to view the app
Open your browser and go to:

```
http://<EC2-IP>:5000
```

You should see:
```
Hello from Sanjay's Flask App!
```

## What I learned
- basics of Flask  
- how Docker works  
- how to install Docker on EC2  
- how to run a container on a cloud server  
- port mapping (5000 to 5000)  
- connecting to EC2 using SSH  

## Things I want to try next
- Nginx reverse proxy  
- GitHub Actions (CI/CD)  
- Deploying using ECS or Kubernetes  
- Adding more features to the Flask app  

## Author
Sanjay
