# kubernetes "example-voting-app"

## Getting started
Make sure **Docker** and **Kubectl** are installed on your system. For windows, prefer "[Docker desktop for Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)".

Go to deployment directory and run following commands on CMD:
1.  `kubectl create -f redis-deployment-definition.yml`
2.  `kubectl create -f postgres-deployment-definition.yml`
3.  `kubectl create -f vote-deployment-definition.yml`
4.  `kubectl create -f result-deployment-definition.yml`
5.  `kubectl create -f worker-deployment-definition.yml`

Go to service directory and run following commands on CMD:
1.  `kubectl create -f redis-service-definition.yml`
2.  `kubectl create -f postgres-service-definition.yml`
3.  `kubectl create -f vote-service-definition.yml`
4.  `kubectl create -f result-service-definition.yml`

Finally, run `kubectl get services` command and see the port of vote and result services. e.g. if ports for vote service is "80:31569" and result service is "80:32204" then app will be running at http://localhost:31569, and the results will be at http://localhost:32204. (Make sure you navigate to the ports on which the services are listening in your system and NOT the ones mentioned above as an example)

## Architecture
![Architecture diagram](architecture.png)

* A Python webapp which lets you vote between two options
* A Redis queue which collects new votes
* A .NET worker which consumes votes and stores them in…
* A Postgres database backed by a Docker volume
* A Node.js webapp which shows the results of the voting in real time

## Note
The voting application only accepts one vote per client. It does not register votes if a vote has already been submitted from a client.
