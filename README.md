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
    app.run(debug=True, host='0.0.0.0')

4. create requirements.txt:

Flask==2.0.2

5. create Dockerfile:

FROM python:latest

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

CMD ["python", "app.py"]

6. open docker desktop
7. docker build -t rhys7homas/kube .
8. docker run -p 5000:5000 rhys7homas/kube    # test it works http://127.0.0.1:5000. ctrl + c in terminal to end
10. docker login
11. docker tag kube rhys7homas/kube:latest
12. docker push rhys7homas/kube:latest      # should now be at https://hub.docker.com/repositories/rhys7homas
13. minikube start  # to install minikube: https://minikube.sigs.k8s.io/docs/start/ # laptop goes really slow
14. kubectl create deployment kube --image=rhys7homas/kube:latest
15. kubectl expose deployment kube --type=NodePort --port=8080
16. minikube service kube
17. kubectl delete deployment kube
18. kubectl delete service kube

im getting a 'problem loading page' page? hmmm
