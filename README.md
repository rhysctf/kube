# kube

1. https://github.com/new
2. vscode > clone repo
3. create app.py:

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=8080)

4. create requirements.txt:

Flask==2.0.2

5. create Dockerfile:

FROM python:latest

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

EXPOSE 8080

CMD ["python", "app.py"]

6. open docker desktop
7. docker build -t kube .
8. docker run -p 5000:5000 rhys7homas/kube    
# test it works http://127.0.0.1:5000. ctrl + c in terminal to end
10. docker login
11. docker tag kube rhys7homas/kube:2.0
12. docker push rhys7homas/kube:2.0      
# should now be at https://hub.docker.com/repositories/rhys7homas

I had to perform these steps to set the env variables for minikube's docker daemon:

@FOR /f "tokens=*" %i IN ('minikube -p minikube docker-env --shell cmd') DO @%i
echo %DOCKER_HOST%      # You should see something like tcp://172.21.154.219:2376

13. minikube start  
# to install minikube: https://minikube.sigs.k8s.io/docs/start/ 
# cmd in administrator mode 
# laptop goes really slow
14. kubectl create deployment test-app --image=rhys7homas/kube:2.0
15. kubectl expose deployment test-app --type=NodePort --port=8080
16. minikube service test-app
17. kubectl delete deployment test-app
18. kubectl delete service test-app
19. minikube stop
