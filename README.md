# docker tutorial

1. Install docker on Ubuntu-18.04
   => [https://phoenixnap.com/kb/how-to-install-docker-on-ubuntu-18-04]

2. show all image
```
docker image ls
```

3. delete image
```
docker image rm [imageName]
```

4. pull hello-world image from dockerhub
```
docker image pull hello-world
```

5. run hello-world by image
```
docker container run hello-world
```

6. run image and simultaniously interactive with a tag, where -it = 'interactive'.
```
docker container run -it ubuntu bash
```

6. show container running now
```
docker container ls
```

7. kill container
```
docker container kill [containerId]
```

8. write Dockerfile
```
FROM python:3.6 # pull image(python:3.6) and add new function on the image
COPY . /app # copy local file to image env
WORKDIR /app # point running path
CMD python3.6 main.py # command
```

9. build image
```
docker image build -t [image-name] . # "." it means building image in now path
```

10. put parameter in code
```
Dockerfile =>
FROM python:3.6
COPY . /app
WORKDIR /app
ENTRYPOINT python3.6 main.py
CMD ['5']
-------------------
main.py =>
import sys
input_level = int(sys.argv[1])
print(input_level)
```

11. docker port : docker port point to localhost port
```
Dockerfile =>
FROM python:3.6
COPY . /app
WORKDIR /app
RUN pip3 install -r requirement.txt
EXPOSE 5000
CMD python3.6 main.py
-------------------
main.py =>
from flask import Flask, render_template
from flask_cors import CORS # need to mention
import json

app = Flask(__name__)
CORS(app)

@app.route('/book')
def json_file():
    file = open('./book.json')
    json_data = json.load(file)
    return json_data

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
=> localhost command : docker container run -p 3000:5000 python-web # 5000->3000
```

11. Manage data in docker (volume) 
```
main.py =>
with open('test.txt','w') as f:
    f.write('finish!!')
-------------------
Dockerfile =>
FROM python:3.6
COPY . /app
WORKDIR /app
CMD python3.6 main.py
-------------------
localhost command =>
docker volume create volume-data # create a volume and its name is volume-data.
docker volume ls # check volume
docker volume inspect volume-data # check specific volume detail information
docker container run -v volume-data:/app/ python-data-volume # -v xx:oo it means 'app/' (docker env) synchronize to volume-data.
docker container run -v volume-data:/volume-data -it ubuntu bash # go to another container(bash) and point volume-data to /volume-data (path)
```

11. Manage data in docker (mint mount) 
```
main.py =>
with open('test.txt','w') as f:
    f.write('finish!!')
-------------------
Dockerfile =>
FROM python:3.6
COPY . /app
WORKDIR /app
CMD python3.6 main.py
-------------------
localhost command =>
docker container run -v localhost_path:/app/ python-data-volume # -v xx:oo it means 'app/' (docker env) synchronize to volume-data.
docker container run -v localhost_path:/volume-data -it ubuntu bash # go to another container(bash) and point volume-data to /volume-data (path)
```

12. docker network (bridge):
```
docker network create --driver bridge [self-def bridge network_name]
docker network ls
docker network inspect [self-def bridge network_name]
docker container run -dit --network [self-def network_name] --name [container_name1] alpine sh
docker container run -dit --network [self-def network_name] --name [container_name2] alpine sh
## test network
docker exec -it [container_name1] sh
ping [container2 network]
docker exec -it [container_name2] sh
ping [container1 network]
```

13. docker network (host):
```
docker network create --driver host [self-def host network_name]
docker network ls
docker network inspect [self-def bridge network_name]
```

