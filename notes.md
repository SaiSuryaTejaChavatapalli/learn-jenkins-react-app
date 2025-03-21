- Running with docker and without docker

```groovy
pipeline {
agent any

    stages {
        stage('Without docker') {
            steps {
               sh 'echo "Without docker" '
            }
        }
        stage('With docker') {
            agent {
                docker{
                    image 'node:18-alpine'
                }
            }
            steps {
                sh 'echo With docker'
                sh '''
                node -v
                npm -v
                '''

            }
        }
    }
}

```

- Creating files with docker and without docker

  ```
  pipeline {
    agent any

    stages {
        stage('Without docker') {
            steps {
               sh '''
               echo "Without docker"
               ls -la
               touch container-no.txt
               '''
            }
        }
        stage('With docker') {
            agent {
                docker{
                    image 'node:18-alpine'
                }
            }
            steps {
                sh '''
                echo "With docker"
                ls -la
                touch container-yes.txt
                '''

            }
        }
    }
  }

  ```

- It will create two workspaces using docker and without docker
- Workspaces for test-node-npm #4
  /var/jenkins_home/workspace/test-node-npm on built-in
  /var/jenkins_home/workspace/test-node-npm@2 on built-in
- to avoid that we should use reuseNode true
  ```
  docker{
       image 'node:18-alpine'
       reuseNode true
       }
  ```
  - now both files will create on same folder
