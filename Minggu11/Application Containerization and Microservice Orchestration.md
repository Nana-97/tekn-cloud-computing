Run 'docker COMMAND --help' for more information on a command.

[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker image build -t linkextractor:step2 .
^[[C^[[CSending build context to Docker daemon    106kB
Step 1/8 : FROM       python:3
 ---> 7f5b6ccd03e9
Step 2/8 : LABEL      maintainer="Sawood Alam <@ibnesayeed>"
 ---> Using cache
 ---> 4d551db7fc88
Step 3/8 : RUN        pip install beautifulsoup4
 ---> Using cache
 ---> b7538d62623e
Step 4/8 : RUN        pip install requests
 ---> Using cache
 ---> 0ea4c3aebc56
Step 5/8 : WORKDIR    /app
 ---> Using cache
 ---> 4927c1ef80db
Step 6/8 : COPY       linkextractor.py /app/
 ---> 13ed933285e8
Step 7/8 : RUN        chmod a+x linkextractor.py
 ---> Running in acf4cdb8154d
Removing intermediate container acf4cdb8154d
 ---> d4ed37201f71
Step 8/8 : ENTRYPOINT ["./linkextractor.py"]
 ---> Running in 3c8bec20c42d
Removing intermediate container 3c8bec20c42d
 ---> f907899b43ba
Successfully built f907899b43ba
Successfully tagged linkextractor:step2
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker container run -it --rm linkextractor:step2 https://training.play-with-docker.com
[Play with Docker classroom](https://training.play-with-docker.com/)
[About](https://training.play-with-docker.com/about/)
[IT Pros and System Administrators](https://training.play-with-docker.com#ops)
[Developers](https://training.play-with-docker.com#dev)
[Stage 1: The Basics](https://training.play-with-docker.com/ops-stage1)
[Stage 2: Digging Deeper](https://training.play-with-docker.com/ops-stage2)
[Stage 3: Moving to Production](https://training.play-with-docker.com/ops-stage3)
[Stage 1: The Basics](https://training.play-with-docker.com/dev-stage1)
[Stage 2: Digging Deeper](https://training.play-with-docker.com/dev-stage2)
[Stage 3: Moving to Staging](https://training.play-with-docker.com/dev-stage3)
[Full list of individual labs](https://training.play-with-docker.com/alacart)
[[IMG]](https://twitter.com/intent/tweet?text=Play with Docker Classroom&url=https://training.play-with-docker.com/&via=docker&related=docker)
[[IMG]](https://facebook.com/sharer.php?u=https://training.play-with-docker.com/)
[[IMG]](https://plus.google.com/share?url=https://training.play-with-docker.com/)
[[IMG]](http://www.linkedin.com/shareArticle?mini=true&url=https://training.play-with-docker.com/&title=Play%20with%20Docker%20Classroom&source=https://training.play-with-docker.com)
[[IMG]](https://www.docker.com/dockercon/)
[Sign up today](https://www.docker.com/dockercon/)
[Register here](https://dockr.ly/slack)
[here](https://www.docker.com/legal/docker-terms-service)
[[IMG]](https://www.docker.com)
[[IMG]](https://www.facebook.com/docker.run)
[[IMG]](https://twitter.com/docker)
[[IMG]](https://www.github.com/play-with-docker/play-with-docker.github.io)
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker container run -it --rm linkextractor:step1 https://training.play-with-docker.com/
/
/about/
#ops
#dev
/ops-stage1
/ops-stage2
/ops-stage3
/dev-stage1
/dev-stage2
/dev-stage3
/alacart
https://twitter.com/intent/tweet?text=Play with Docker Classroom&url=https://training.play-with-docker.com/&via=docker&related=docker
https://facebook.com/sharer.php?u=https://training.play-with-docker.com/
https://plus.google.com/share?url=https://training.play-with-docker.com/
http://www.linkedin.com/shareArticle?mini=true&url=https://training.play-with-docker.com/&title=Play%20with%20Docker%20Classroom&source=https://training.play-with-docker.com
https://www.docker.com/dockercon/
https://www.docker.com/dockercon/
https://dockr.ly/slack
https://www.docker.com/legal/docker-terms-service
https://www.docker.com
https://www.facebook.com/docker.run
https://twitter.com/docker
https://www.github.com/play-with-docker/play-with-docker.github.io
[node1] (local) root@192.168.0.23 ~/linkextractor
$ git checkout step3
Branch 'step3' set up to track remote branch 'step3' from 'origin'.
Switched to a new branch 'step3'
[node1] (local) root@192.168.0.23 ~/linkextractor
$ tree
.
├── Dockerfile
├── README.md
├── linkextractor.py
├── main.py
└── requirements.txt

0 directories, 5 files
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat Dockerfile
FROM       python:3
LABEL      maintainer="Sawood Alam <@ibnesayeed>"

WORKDIR    /app
COPY       requirements.txt /app/
RUN        pip install -r requirements.txt

COPY       *.py /app/
RUN        chmod a+x *.py

CMD        ["./main.py"]
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat mani.py
cat: can't open 'mani.py': No such file or directory
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat main.py
#!/usr/bin/env python

from flask import Flask
from flask import request
from flask import jsonify
from linkextractor import extract_links

app = Flask(__name__)

@app.route("/")
def index():
    return "Usage: http://<hostname>[:<prt>]/api/<url>"

@app.route("/api/<path:url>")
def api(url):
    qs = request.query_string.decode("utf-8")
    if qs != "":
        url += "?" + qs
    links = extract_links(url)
    return jsonify(links)

app.run(host="0.0.0.0")
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker image build -t linkextractor:step3 .
Sending build context to Docker daemon  110.6kB
Step 1/8 : FROM       python:3
 ---> 7f5b6ccd03e9
Step 2/8 : LABEL      maintainer="Sawood Alam <@ibnesayeed>"
 ---> Using cache
 ---> 4d551db7fc88
Step 3/8 : WORKDIR    /app
 ---> Running in 840296e2ae9e
Removing intermediate container 840296e2ae9e
 ---> 01df149e74de
Step 4/8 : COPY       requirements.txt /app/
 ---> 26ec65aa727e
Step 5/8 : RUN        pip install -r requirements.txt
 ---> Running in bc0401af8fea
Collecting beautifulsoup4
  Downloading beautifulsoup4-4.9.1-py3-none-any.whl (115 kB)
Collecting flask
  Downloading Flask-1.1.2-py2.py3-none-any.whl (94 kB)
Collecting requests
  Downloading requests-2.23.0-py2.py3-none-any.whl (58 kB)
Collecting soupsieve>1.2
  Downloading soupsieve-2.0.1-py3-none-any.whl (32 kB)
Collecting click>=5.1
  Downloading click-7.1.2-py2.py3-none-any.whl (82 kB)
Collecting itsdangerous>=0.24
  Downloading itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Collecting Werkzeug>=0.15
  Downloading Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Collecting Jinja2>=2.10.1
  Downloading Jinja2-2.11.2-py2.py3-none-any.whl (125 kB)
Collecting chardet<4,>=3.0.2
  Downloading chardet-3.0.4-py2.py3-none-any.whl (133 kB)
Collecting urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1
  Downloading urllib3-1.25.9-py2.py3-none-any.whl (126 kB)
Collecting certifi>=2017.4.17
  Downloading certifi-2020.4.5.2-py2.py3-none-any.whl (157 kB)
Collecting idna<3,>=2.5
  Downloading idna-2.9-py2.py3-none-any.whl (58 kB)
Collecting MarkupSafe>=0.23
  Downloading MarkupSafe-1.1.1-cp38-cp38-manylinux1_x86_64.whl (32 kB)
Installing collected packages: soupsieve, beautifulsoup4, click, itsdangerous, Werkzeug, MarkupSafe, Jinja2, flask, chardet, urllib3, certifi, idna, requests
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1 Werkzeug-1.0.1 beautifulsoup4-4.9.1 certifi-2020.4.5.2 chardet-3.0.4 click-7.1.2 flask-1.1.2 idna-2.9 itsdangerous-1.1.0 requests-2.23.0 soupsieve-2.0.1 urllib3-1.25.9
Removing intermediate container bc0401af8fea
 ---> 3361e8e1be0f
Step 6/8 : COPY       *.py /app/
 ---> 54979f4d42ff
Step 7/8 : RUN        chmod a+x *.py
 ---> Running in 7109e8c5d7ec
Removing intermediate container 7109e8c5d7ec
 ---> b824822c1bb3
Step 8/8 : CMD        ["./main.py"]
 ---> Running in 2e8a0f1681bd
Removing intermediate container 2e8a0f1681bd
 ---> a9053ccb1b09
Successfully built a9053ccb1b09
Successfully tagged linkextractor:step3
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker container run -d -p 5000:5000 --name=linkextractor linkextractor:step3
57e9324c3750ae7bf6721c37c51b3421f9c5cac8bb90665856127898c434b790
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker container ls
CONTAINER ID        IMAGE                 COMMAND             CREATED           STATUS              PORTS                    NAMES
57e9324c3750        linkextractor:step3   "./main.py"         17 seconds ago      Up 16 seconds       0.0.0.0:5000->5000/tcp   linkextractor
[node1] (local) root@192.168.0.23 ~/linkextractor
$ curl -i http://localhost:5000/api/http://example.com/
HTTP/1.0 200 OK
Content-Type: application/json
Content-Length: 79
Server: Werkzeug/1.0.1 Python/3.8.3
Date: Wed, 10 Jun 2020 10:32:10 GMT

[{"href":"https://www.iana.org/domains/example","text":"More information..."}]
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker container logs linkextractor
 * Serving Flask app "main" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
172.17.0.1 - - [10/Jun/2020 10:32:10] "GET /api/http://example.com/ HTTP/1.1" 200 -
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker container rm -f linkextractor
linkextractor
[node1] (local) root@192.168.0.23 ~/linkextractor
$ git checkout step4
Branch 'step4' set up to track remote branch 'step4' from 'origin'.
Switched to a new branch 'step4'
[node1] (local) root@192.168.0.23 ~/linkextractor
$ tree
.
├── README.md
├── api
│   ├── Dockerfile
│   ├── linkextractor.py
│   ├── main.py
│   └── requirements.txt
├── docker-compose.yml
└── www
    └── index.php

2 directories, 7 files
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat docker-compose.yml
version: '3'

services:
  api:
    image: linkextractor-api:step4-python
    build: ./api
    ports:
      - "5000:5000"
  web:
    image: php:7-apache
    ports:
      - "80:80"
    environment:
      - API_ENDPOINT=http://api:5000/api/
    volumes:
      - ./www:/var/www/html
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat www/index.php
<!DOCTYPE html>

<?php
  $api_endpoint = $_ENV["API_ENDPOINT"] ?: "http://localhost:5000/api/";
  $url = "";
  if(isset($_GET["url"]) && $_GET["url"] != "") {
    $url = $_GET["url"];
    $json = @file_get_contents($api_endpoint . $url);
    if($json == false) {
      $err = "Something is wrong with the URL: " . $url;
    } else {
      $links = json_decode($json, true);
      $domains = [];
      foreach($links as $link) {
        array_push($domains, parse_url($link["href"], PHP_URL_HOST));
      }
      $domainct = @array_count_values($domains);
      arsort($domainct);
    }
  }
?>

<html>
  <head>
    <meta charset="utf-8">
    <title>Link Extractor</title>
    <style media="screen">
      html {
        background: #EAE7D6;
        font-family: sans-serif;
      }
      body {
        margin: 0;
      }
      h1 {
        padding: 10px;
        margin: 0 auto;
        color: #EAE7D6;
        max-width: 600px;
      }
      h1 a {
        text-decoration: none;
        color: #EAE7D6;
      }
      h2 {
        background: #082E41;
        color: #EAE7D6;
        margin: -10px;
        padding: 10px;
      }
      p {
        margin: 25px 5px 5px;
      }
      section {
        max-width: 600px;
        margin: 10px auto;
        padding: 10px;
        border: 1px solid #082E41;
      }
      div.header {
        background: #082E41;
        margin: 0;
      }
      div.footer {
        background: #082E41;
        margin: 0;
        padding: 5px;
      }
      .footer p {
        margin: 0 auto;
        max-width: 600px;
        color: #EAE7D6;
        text-align: center;
      }
      .footer p a {
        color: #24C2CB;
        text-decoration: none;
      }
      .error {
        color: #DA2536;
      }
      form {
        display: flex;
      }
      input {
        font-size: 20px;
        padding: 3px;
        height: 40px;
      }
      input.text {
        box-sizing:border-box;
        flex-grow: 1;
        border-color: #082E41;
      }
      input.button {
        width: 150px;
        background: #082E41;
        border-color: #082E41;
        color: #EAE7D6;
      }
      table {
        width: 100%;
        text-align: left;
        margin-top: 10px;
      }
      table th, table td {
        padding: 3px;
      }
      table th:last-child, table td:last-child {
        width: 70px;
        text-align: right;
      }
      table th {
        border-top: 1px solid #082E41;
        border-bottom: 1px solid #082E41;
      }
      table tr:last-child td {
        border-top: 1px solid #082E41;
        border-bottom: 1px solid #082E41;
      }
    </style>
  </head>
  <body>
    <div class="header">
      <h1><a href="/">Link Extractor</a></h1>
    </div>

    <section>
      <form action="/">
        <input class="text" type="text" name="url" placeholder="http://example.com/" value="<?php echo $url; ?>">
        <input class="button" type="submit" value="Extract Links">
      </form>
    </section>

    <?php if(isset($err)): ?>
      <section>
        <h2>Error</h2>
        <p class="error"><?php echo $err; ?></p>
      </section>
    <?php endif; ?>

    <?php if($url != "" && !isset($err)): ?>
      <section>
        <h2>Summary</h2>
        <p>
          <strong>Page:</strong> <?php echo "<a href=\"" . $url . "\">" . $url . "</a>"; ?>
        </p>
        <table>
          <tr>
            <th>Domain</th>
            <th># Links</th>
          </tr>
          <?php
            foreach($domainct as $key => $value) {
              echo "<tr>";
              echo "<td>" . $key . "</td>";
              echo "<td>" . $value . "</td>";
              echo "</tr>";
            }
          ?>
          <tr>
            <td><strong>Total</strong></td>
            <td><strong><?php echo count($links); ?></strong></td>
          </tr>
        </table>
      </section>

      <section>
        <h2>Links</h2>
        <ul>
        <?php
          foreach($links as $link) {
            echo "<li><a href=\"" . $link["href"] . "\">" . $link["text"] . "</a></li>";
          }
        ?>
        </ul>
      </section>
    <?php endif; ?>

    <div class="footer">
      <p><a href="https://github.com/ibnesayeed/linkextractor">Link Extractor</a> by <a href="https://twitter.com/ibnesayeed">@ibnesayeed</a>from
        <a href="https://ws-dl.cs.odu.edu/">WS-DL, ODU</a>
      </p>
    </div>
  </body>
</html>
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker-compose up -d --build
Creating network "linkextractor_default" with the default driver
Building api
Step 1/8 : FROM       python:3
 ---> 7f5b6ccd03e9
Step 2/8 : LABEL      maintainer="Sawood Alam <@ibnesayeed>"
 ---> Using cache
 ---> 4d551db7fc88
Step 3/8 : WORKDIR    /app
 ---> Using cache
 ---> 01df149e74de
Step 4/8 : COPY       requirements.txt /app/
 ---> c40f8227e8a5
Step 5/8 : RUN        pip install -r requirements.txt
 ---> Running in 80d011919518
Collecting beautifulsoup4
  Downloading beautifulsoup4-4.9.1-py3-none-any.whl (115 kB)
Collecting flask
  Downloading Flask-1.1.2-py2.py3-none-any.whl (94 kB)
Collecting requests
  Downloading requests-2.23.0-py2.py3-none-any.whl (58 kB)
Collecting soupsieve>1.2
  Downloading soupsieve-2.0.1-py3-none-any.whl (32 kB)
Collecting Jinja2>=2.10.1
  Downloading Jinja2-2.11.2-py2.py3-none-any.whl (125 kB)
Collecting itsdangerous>=0.24
  Downloading itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Collecting Werkzeug>=0.15
  Downloading Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Collecting click>=5.1
  Downloading click-7.1.2-py2.py3-none-any.whl (82 kB)
Collecting idna<3,>=2.5
  Downloading idna-2.9-py2.py3-none-any.whl (58 kB)
Collecting certifi>=2017.4.17
  Downloading certifi-2020.4.5.2-py2.py3-none-any.whl (157 kB)
Collecting urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1
  Downloading urllib3-1.25.9-py2.py3-none-any.whl (126 kB)
Collecting chardet<4,>=3.0.2
  Downloading chardet-3.0.4-py2.py3-none-any.whl (133 kB)
Collecting MarkupSafe>=0.23
  Downloading MarkupSafe-1.1.1-cp38-cp38-manylinux1_x86_64.whl (32 kB)
Installing collected packages: soupsieve, beautifulsoup4, MarkupSafe, Jinja2, itsdangerous, Werkzeug, click, flask, idna, certifi, urllib3, chardet, requests
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1 Werkzeug-1.0.1 beautifulsoup4-4.9.1 certifi-2020.4.5.2 chardet-3.0.4 click-7.1.2 flask-1.1.2 idna-2.9 itsdangerous-1.1.0 requests-2.23.0 soupsieve-2.0.1 urllib3-1.25.9
Removing intermediate container 80d011919518
 ---> ae4101adae1f
Step 6/8 : COPY       *.py /app/
 ---> f29cd3457987
Step 7/8 : RUN        chmod a+x *.py
 ---> Running in a39bc7d71f2a
Removing intermediate container a39bc7d71f2a
 ---> 82f7457a1414
Step 8/8 : CMD        ["./main.py"]
 ---> Running in 34c5f0bc706c
Removing intermediate container 34c5f0bc706c
 ---> de5f0f98d698
Successfully built de5f0f98d698
Successfully tagged linkextractor-api:step4-python
Pulling web (php:7-apache)...
7-apache: Pulling from library/php
8559a31e96f4: Pull complete
e0276193a084: Pull complete
eb2d00c10344: Pull complete
f54006e0dc29: Pull complete
e0d3d1244592: Pull complete
3a60f364b0c5: Pull complete
3e309988c00b: Pull complete
5d92b4c08548: Pull complete
83faa9e6981c: Pull complete
8f4f490c1749: Pull complete
e75eda9c13c2: Pull complete
af5ca20c6fe0: Pull complete
ecf22074a2a4: Pull complete
Digest: sha256:8b741fab33229187b2bc161b2176ba07997664d00a778c0a7df59514440f0acc
Status: Downloaded newer image for php:7-apache
Creating linkextractor_web_1 ... done
Creating linkextractor_api_1 ... done
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker container ls
CONTAINER ID        IMAGE                            COMMAND       CREATED             STATUS              PORTS NAMES
4bc79f7ff60d        linkextractor-api:step4-python   "./main.py"       28 seconds ago      Up 27 seconds       0.0.0.0:5000->5000/tcp linkextractor_api_1
76f47ab3e119        php:7-apache                     "docker-php-entrypoi…"   28 seconds ago      Up 26 seconds       0.0.0.0:80->80/tcp linkextractor_web_1
[node1] (local) root@192.168.0.23 ~/linkextractor
$ curl -i http://localhost:5000/api/http://example.com/
HTTP/1.0 200 OK
Content-Type: application/json
Content-Length: 79
Server: Werkzeug/1.0.1 Python/3.8.3
Date: Wed, 10 Jun 2020 10:36:12 GMT

[{"href":"https://www.iana.org/domains/example","text":"More information..."}]
[node1] (local) root@192.168.0.23 ~/linkextractor
$ sed -i 's/Link Extractor/Super Link Extractor/g' wwwn/index.php
sed: wwwn/index.php: No such file or directory
[node1] (local) root@192.168.0.23 ~/linkextractor
$ git retse --hard
git: 'retse' is not a git command. See 'git --help'.

The most similar command is
        restore
[node1] (local) root@192.168.0.23 ~/linkextractor
$ git reset --hard
HEAD is now at 2a3ec3e Synchronize branch step4
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker-compose down
Stopping linkextractor_api_1 ... done
Stopping linkextractor_web_1 ... done
Removing linkextractor_api_1 ... done
Removing linkextractor_web_1 ... done
Removing network linkextractor_default
[node1] (local) root@192.168.0.23 ~/linkextractor
$ git checkout step5
Branch 'step5' set up to track remote branch 'step5' from 'origin'.
Switched to a new branch 'step5'
[node1] (local) root@192.168.0.23 ~/linkextractor
$ tree
.
├── README.md
├── api
│   ├── Dockerfile
│   ├── linkextractor.py
│   ├── main.py
│   └── requirements.txt
├── docker-compose.yml
└── www
    ├── Dockerfile
    └── index.php

2 directories, 8 files
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat www/Dockerfile
FROM       php:7-apache
LABEL      maintainer="Sawood Alam <@ibnesayeed>"

ENV        API_ENDPOINT="http://localhost:5000/api/"

COPY       . /var/www/html/
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat api/main.py
#!/usr/bin/env python

import os
import json
import redis
from flask import Flask
from flask import request
from linkextractor import extract_links

app = Flask(__name__)
redis_conn = redis.from_url(os.getenv("REDIS_URL", "redis://localhost:6379"))

@app.route("/")
def index():
    return "Usage: http://<hostname>[:<prt>]/api/<url>"

@app.route("/api/<path:url>")
def api(url):
    qs = request.query_string.decode("utf-8")
    if qs != "":
        url += "?" + qs

    jsonlinks = redis_conn.get(url)
    if not jsonlinks:
        links = extract_links(url)
        jsonlinks = json.dumps(links, indent=2)
        redis_conn.set(url, jsonlinks)

    response = app.response_class(
        status=200,
        mimetype="application/json",
        response=jsonlinks
    )

    return response

app.run(host="0.0.0.0")
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat docker-compose.yml
version: '3'

services:
  api:
    image: linkextractor-api:step5-python
    build: ./api
    ports:
      - "5000:5000"
    environment:
      - REDIS_URL=redis://redis:6379
  web:
    image: linkextractor-web:step5-php
    build: ./www
    ports:
      - "80:80"
    environment:
      - API_ENDPOINT=http://api:5000/api/
  redis:
    image: redis
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker-compose up -d --build
Creating network "linkextractor_default" with the default driver
Building api
Step 1/9 : FROM       python:3
 ---> 7f5b6ccd03e9
Step 2/9 : LABEL      maintainer="Sawood Alam <@ibnesayeed>"
 ---> Using cache
 ---> 4d551db7fc88
Step 3/9 : ENV        REDIS_URL="redis://localhost:6379"
 ---> Running in 5b4dd9215401
Removing intermediate container 5b4dd9215401
 ---> 570fbdfd8a0c
Step 4/9 : WORKDIR    /app
 ---> Running in 1d8c24924560
Removing intermediate container 1d8c24924560
 ---> 9f412a1e86af
Step 5/9 : COPY       requirements.txt /app/
 ---> 1f9ff00ed4d2
Step 6/9 : RUN        pip install -r requirements.txt
 ---> Running in 5df6ff71b257
Collecting beautifulsoup4
  Downloading beautifulsoup4-4.9.1-py3-none-any.whl (115 kB)
Collecting flask
  Downloading Flask-1.1.2-py2.py3-none-any.whl (94 kB)
Collecting redis
  Downloading redis-3.5.3-py2.py3-none-any.whl (72 kB)
Collecting requests
  Downloading requests-2.23.0-py2.py3-none-any.whl (58 kB)
Collecting soupsieve>1.2
  Downloading soupsieve-2.0.1-py3-none-any.whl (32 kB)
Collecting itsdangerous>=0.24
  Downloading itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Collecting Jinja2>=2.10.1
  Downloading Jinja2-2.11.2-py2.py3-none-any.whl (125 kB)
Collecting click>=5.1
  Downloading click-7.1.2-py2.py3-none-any.whl (82 kB)
Collecting Werkzeug>=0.15
  Downloading Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Collecting certifi>=2017.4.17
  Downloading certifi-2020.4.5.2-py2.py3-none-any.whl (157 kB)
Collecting idna<3,>=2.5
  Downloading idna-2.9-py2.py3-none-any.whl (58 kB)
Collecting chardet<4,>=3.0.2
  Downloading chardet-3.0.4-py2.py3-none-any.whl (133 kB)
Collecting urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1
  Downloading urllib3-1.25.9-py2.py3-none-any.whl (126 kB)
Collecting MarkupSafe>=0.23
  Downloading MarkupSafe-1.1.1-cp38-cp38-manylinux1_x86_64.whl (32 kB)
Installing collected packages: soupsieve, beautifulsoup4, itsdangerous, MarkupSafe, Jinja2, click, Werkzeug, flask, redis, certifi, idna, chardet, urllib3, requests
Successfully installed Jinja2-2.11.2 MarkupSafe-1.1.1 Werkzeug-1.0.1 beautifulsoup4-4.9.1 certifi-2020.4.5.2 chardet-3.0.4 click-7.1.2 flask-1.1.2 idna-2.9 itsdangerous-1.1.0 redis-3.5.3 requests-2.23.0 soupsieve-2.0.1 urllib3-1.25.9
Removing intermediate container 5df6ff71b257
 ---> d5782d8a3926
Step 7/9 : COPY       *.py /app/
 ---> a68e242d30c5
Step 8/9 : RUN        chmod a+x *.py
 ---> Running in 6fb3668eeecb
Removing intermediate container 6fb3668eeecb
 ---> 4558ccfacb9b
Step 9/9 : CMD        ["./main.py"]
 ---> Running in b9960065047e
Removing intermediate container b9960065047e
 ---> 831a196c8edc
Successfully built 831a196c8edc
Successfully tagged linkextractor-api:step5-python
Building web
Step 1/4 : FROM       php:7-apache
 ---> 11fe2f85b3de
Step 2/4 : LABEL      maintainer="Sawood Alam <@ibnesayeed>"
 ---> Running in b0b5b1f020bf
Removing intermediate container b0b5b1f020bf
 ---> ea632ba48e1f
Step 3/4 : ENV        API_ENDPOINT="http://localhost:5000/api/"
 ---> Running in c59439d69c92
Removing intermediate container c59439d69c92
 ---> cbbbb7f9531d
Step 4/4 : COPY       . /var/www/html/
 ---> 95282c392568
Successfully built 95282c392568
Successfully tagged linkextractor-web:step5-php
Pulling redis (redis:)...
latest: Pulling from library/redis
8559a31e96f4: Already exists
85a6a5c53ff0: Pull complete
b69876b7abed: Pull complete
a72d84b9df6a: Pull complete
5ce7b314b19c: Pull complete
04c4bfb0b023: Pull complete
Digest: sha256:02ad2f2ddb16dc8f3b57a6b03f053aa1554735513af896b972b1887a5400fc37
Status: Downloaded newer image for redis:latest
Creating linkextractor_web_1   ... done
Creating linkextractor_api_1   ... done
Creating linkextractor_redis_1 ... done
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker-compose exec redis redis-cli monitor
OK
^C[node1] (local) root@192.168.0.23 ~/linkextractor
$ sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php
[node1] (local) root@192.168.0.23 ~/linkextractor
$ git reset --hard
HEAD is now at 3dbb7eb Synchronize branch step5
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker-compose down
Stopping linkextractor_redis_1 ... done
Stopping linkextractor_api_1   ... done
Stopping linkextractor_web_1   ... done
Removing linkextractor_redis_1 ... done
Removing linkextractor_api_1   ... done
Removing linkextractor_web_1   ... done
Removing network linkextractor_default
[node1] (local) root@192.168.0.23 ~/linkextractor
$ git checkout step6
Branch 'step6' set up to track remote branch 'step6' from 'origin'.
Switched to a new branch 'step6'
[node1] (local) root@192.168.0.23 ~/linkextractor
$ tree
.
├── README.md
├── api
│   ├── Dockerfile
│   ├── Gemfile
│   └── linkextractor.rb
├── docker-compose.yml
├── logs
└── www
    ├── Dockerfile
    └── index.php

3 directories, 7 files
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat api/linkextractor.rb
#!/usr/bin/env ruby
# encoding: utf-8

require "sinatra"
require "open-uri"
require "uri"
require "nokogiri"
require "json"
require "redis"

set :protection, :except=>:path_traversal

redis = Redis.new(url: ENV["REDIS_URL"] || "redis://localhost:6379")

Dir.mkdir("logs") unless Dir.exist?("logs")
cache_log = File.new("logs/extraction.log", "a")

get "/" do
  "Usage: http://<hostname>[:<prt>]/api/<url>"
end

get "/api/*" do
  url = [params['splat'].first, request.query_string].reject(&:empty?).join("?")
  cache_status = "HIT"
  jsonlinks = redis.get(url)
  if jsonlinks.nil?
    cache_status = "MISS"
    jsonlinks = JSON.pretty_generate(extract_links(url))
    redis.set(url, jsonlinks)
  end

  cache_log.puts "#{Time.now.to_i}\t#{cache_status}\t#{url}"

  status 200
  headers "content-type" => "application/json"
  body jsonlinks
end

def extract_links(url)
  links = []
  doc = Nokogiri::HTML(open(url))
  doc.css("a").each do |link|
    text = link.text.strip.split.join(" ")
    begin
      links.push({
        text: text.empty? ? "[IMG]" : text,
        href: URI.join(url, link["href"])
      })
    rescue
    end
  end
  links
end
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat api/Dockerfile
FROM       ruby:2.6
LABEL      maintainer="Sawood Alam <@ibnesayeed>"

ENV        LANG C.UTF-8
ENV        REDIS_URL="redis://localhost:6379"

WORKDIR    /app
COPY       Gemfile /app/
RUN        bundle install

COPY       linkextractor.rb /app/
RUN        chmod a+x linkextractor.rb

CMD        ["./linkextractor.rb", "-o", "0.0.0.0"]
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat docker-compose.yml
version: '3'

services:
  api:
    image: linkextractor-api:step6-ruby
    build: ./api
    ports:
      - "4567:4567"
    environment:
      - REDIS_URL=redis://redis:6379
    volumes:
      - ./logs:/app/logs
  web:
    image: linkextractor-web:step6-php
    build: ./www
    ports:
      - "80:80"
    environment:
      - API_ENDPOINT=http://api:4567/api/
  redis:
    image: redis
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker-compose up -d --build
Creating network "linkextractor_default" with the default driver
Building api
Step 1/10 : FROM       ruby:2.6
2.6: Pulling from library/ruby
e9afc4f90ab0: Already exists
989e6b19a265: Already exists
af14b6c2f878: Already exists
5573c4b30949: Already exists
11a88e764313: Already exists
7bab57a324dc: Pull complete
8c5617e2c165: Pull complete
f6db801ee73f: Pull complete
Digest: sha256:8a4d9012682440bdd1ad74c84ca72f8f94677c075452ec7e3692b03bdbb5e761
Status: Downloaded newer image for ruby:2.6
 ---> cf2f8e029dad
Step 2/10 : LABEL      maintainer="Sawood Alam <@ibnesayeed>"
 ---> Running in 52d715715c51
Removing intermediate container 52d715715c51
 ---> fe74ad3ea636
Step 3/10 : ENV        LANG C.UTF-8
 ---> Running in 63752637e400
Removing intermediate container 63752637e400
 ---> 1d0d1e454bb0
Step 4/10 : ENV        REDIS_URL="redis://localhost:6379"
 ---> Running in 9446ff6d0ee9
Removing intermediate container 9446ff6d0ee9
 ---> f962d417782f
Step 5/10 : WORKDIR    /app
 ---> Running in 41b59a96ea40
Removing intermediate container 41b59a96ea40
 ---> 7b9795c8ee57
Step 6/10 : COPY       Gemfile /app/
 ---> 532e1d70e6b2
Step 7/10 : RUN        bundle install
 ---> Running in 93d19cc6590e
Fetching gem metadata from https://rubygems.org/.......
Resolving dependencies...
Using bundler 1.17.2
Fetching mini_portile2 2.4.0
Installing mini_portile2 2.4.0
Fetching ruby2_keywords 0.0.2
Installing ruby2_keywords 0.0.2
Fetching mustermann 1.1.1
Installing mustermann 1.1.1
Fetching nokogiri 1.10.9
Installing nokogiri 1.10.9 with native extensions
^CERROR: Aborting.
[node1] (local) root@192.168.0.23 ~/linkextractor
$ curl -1 http://localhost:4567/api/http://example.com/
curl: (7) Failed to connect to localhost port 4567: Connection refused
[node1] (local) root@192.168.0.23 ~/linkextractor
$ docker-compose down
Removing network linkextractor_default
[node1] (local) root@192.168.0.23 ~/linkextractor
$ cat logs/extraction.log
cat: can't open 'logs/extraction.log': No such file or directory
