---
layout: post
title: "Jenkins Rails Docker container"
date: 2015-05-04 12:25:29 +0300
comments: true
categories: docker ci
---

Today I want to present my first contribution to Docker community - 
[Jenkins Rails image](https://registry.hub.docker.com/u/goodniceweb/jenkins-rails/). 

For better understanding what work was done I propose to look into 
[Dockerfile](https://github.com/goodniceweb/docker-jenkins-rails/blob/master/Dockerfile). 
At first lines you can see system upgrades, installing Rails requirements 
and npm. Secondly, we ignore auto generated docs and install useful plugins.

That's it! Is it so little? Maybe, but it's enough for start. Almost.

Are you want to know how to use and extend it for your needs? 
What are you waiting for - press a "Read more" button.

<!--more-->

How to use
----------

```bash
docker run -p 8080:8080 \
           -v /your/host/volume:/home/jenkins_home \
           goodniceweb/jenkins-rails:latest
```

Visit `your.domain.example:8080` and voila: here is Jenkins 
prepared for your Rails project!


How to extend
-------------

In few cases you find something missing in this based image. 
Fortunately, it's easy to extend.

Firstly, create your own Dockerfile.

```bash
FROM goodniceweb/jenkins-rails:latest
MAINTAINER Your Name <your@email>

# capybara requirements
# RUN npm install -g phantomjs

# dependencies of running javascript test on instances without X 
# RUN apt-get install -y vnc4server 

# help to avoid error MoveTargetOutOfBoundsError
# RUN apt-get install -y fluxbox

# rmagick dependencies
# RUN apt-get install -y imagemagick

# dependencies of capybara webkit gem
# RUN apt-get install -y libqt4-dev libqtwebkit-dev

# Good practice - drop back to regular user
USER jenkins

ENTRYPOINT ["/usr/local/bin/jenkins.sh"]
```

I think above comments are very self explain.

Secondly, run `docker build` command. For ex.

```bash
docker build -t my-nick/my-jenkins-build:latest .
```

Finally, just run it.

```bash
docker run -p 8080:8080 \
           -v /your/host/volume:/home/jenkins_home \
           my-nick/my-jenkins-build:latest
```

That's it! So easy, isn't?

I hope you find it useful. Have a nice web!

