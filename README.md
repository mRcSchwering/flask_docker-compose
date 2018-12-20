# How to connect to flask in docker-compose

Normally starting app and curling on host works.

```
python3 app.py
...
curl -i http://0.0.0.0:5000
...
200 - ok
```

Running flask app in a container and curling from host also works.

```
docker build -t flask_test .
docker run --rm -p 5000:5000 flask_test
...
curl -i http://0.0.0.0:5000
...
200 - ok
```

Starting flask app as service via docker-compose, then curling
from host also works.

```
docker-compose build
docker-compose up
...
curl -i http://0.0.0.0:5000
...
200 - ok
```

But starting flask app as service via docker-compose,
then curling from another container doesn't work.

```
docker-compose build
docker-compose up
...
docker-compose run test sh
# apk --update add curl
# curl -i http://app:5000
...
404 - not found
```

Docker-compose built a bridge to connect `app` and `test`,
and by the logs from `app` you can also see that the requests are
comming in (and responded with 404).
