# Jenkins
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Jenkins](#jenkins)
	- [Installation](#installation)
		- [Get InitialAdminPassword](#get-initialadminpassword)
	- [Pipeline](#pipeline)

<!-- /TOC -->
## Installation
Install Jenkins in the docker

```sh
docker pull jenkins
```

Run jenkins with assgined port `49001:8080`

```sh
docker run -d -p 49001:8080 -v $PWD/jenkins:/var/jenkins_home:z -t jenkins
```

Visit `localhost:49001` and config the jenkins.

### Get InitialAdminPassword

Find the id of jenkins instance
```sh
docker ps -a
```

Get the shell of that instance, in here, my instance id is `26f8fda57fad`
```sh
docker exec -it 26f8fda57fad bash
```

Then you should be able to obtain the InitialAdminPassword

## Pipeline
View [Official Doc](https://jenkins.io/doc/pipeline/tour/hello-world/) for more information

Create new file `Jenkinsfile` with content (This is for naive implementation, the example is in my git repository [here](https://github.com/Kai5174/JenkinsLearning))
```
pipeline {
    agent { docker 'python:3.5.1' }
    stages {
        stage('build') {
            steps {
                sh 'python --version'
                sh 'ls'
            }
        }
    }
}
```

push it into your git repository.
```sh
git push origin master
```

Then go to the `localhost:49001`, choose new Item, with `multiPipelines` properties, then config the rules and access credential. Now the Jenkins should be work
