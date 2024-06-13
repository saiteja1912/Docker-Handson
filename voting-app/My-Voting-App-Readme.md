Deploying Voting app with docker cmds(Without using docker swarm):
--------------------------------------
* move to vote dir
* docker build -t voting-app .
* docker run -d  --name=redis redis
* docker run -d -p 5000:80 --link redis:redis voting-app
* docker run -d --name=db postgres:9.4
* move to worker dir
* docker build -t worker-app .
* docker run -d --link redis:redis --link db:db worker-app
* move to result dir
* docker build -t result-app .
* docker run -p 5001:80 --link db:db result-app

Voting app is hosted on <node_ip>:5000
Result app is hosted on <node_ip>:5001