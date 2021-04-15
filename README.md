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
```










