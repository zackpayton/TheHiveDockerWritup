# TheHiveDockerWritup
A brief writeup of how to build your own docker container for TheHive


This writeup will walk us through creating a local docker version of TheHive useful for local feature development.

Some assumptions:
* Running on an OSX machine
* Already have docker installed
* Already have brew installed
* Already have sbt installed (scala build tool)
* Alreday have npm installed (installed with brew)
* Already have grunt-cli installed (installed with npm)
* Already have bower installed (I did it with npm)

1. Clone TheHive repository:
```git clone https://github.com/TheHive-Project/TheHive```

2. Change Directory into TheHive:
```cd TheHive```

3. Make your code changes:
An example:
```sed -i '' 's/Summary/My Summary/' ui/app/views/partials/case/case.details.html```

4. Create the docker package:
```bin/activator docker:stage```

5. Build the docker container and add a useful tag if you want:
```cd target/docker/stage/; docker build . -t myhive```

6. Make sure your image is installed in your local docker repository:
```docker image ls```

7. Modify TheHive/docker/thehive/docker-compose.yml to load your container instead of the community container:
```cd ../../..; sed -i '' 's/certbdf\/thehive:latest/myhive/' docker/thehive/docker-compose.yml```

8. Start your modified version of TheHive in a local docker container:
```cd docker/thehive; docker-compose up```
