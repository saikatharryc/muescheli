# muescheli
("müscheli" is swiss german for a small sea shell or clam)

**small service that connects to a ClamAV daemon through tcp**

## test locally

use the `docker-compose.yml`
```bash
$ docker-compose up --build
```

*or*

build ClamAV image and run
```bash
$ docker build -t clamav clamav
$ docker run -p 3310:3310 clamav
```

run the webservice (requires a go installation with dep)
```bash
$ dep ensure
$ go run main.go
```

run a test
```bash
$ curl -v -u muescheli:muescheli -X POST -H "Content-Type: multipart/form-data" -F "file1=@test/eicar.com" -F "file2=@test/test.txt"  http://localhost:8091/scan
```
or
```bash
$ curl -v -u muescheli:muescheli -X PUT --data-binary @test/eicar.com http://localhost:8091/scan
```
or
```bash
$ curl -u muescheli:muescheli -v http://localhost:8091/scan?url=https://tech.ebu.ch/docs/tech/tech3285.pdf
```

## run on kubernetes
```bash
$ kubectl create -f k8s/deployment.yml
```
this will start a pod with 2 containers (clamav and muescheli)

muescheli service exposed through random NodePort port


Ref:

- https://github.com/lastops/muescheli
- https://github.com/monostream/muescheli
