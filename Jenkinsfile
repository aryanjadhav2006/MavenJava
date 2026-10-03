pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Git Clone & Clean') {
            steps {
                sh 'rm -rf MavenJava'
                sh 'git clone https://github.com/aryanjadhav2006/MavenJava.git'
                sh '/opt/homebrew/bin/mvn clean -f MavenJava'
            }
        }

        stage('Install') {
            steps {
                sh '/opt/homebrew/bin/mvn install -f MavenJava'
            }
        }

        stage('Test') {
            steps {
                sh '/opt/homebrew/bin/mvn test -f MavenJava'
            }
        }

        stage('Package') {
            steps {
                sh '/opt/homebrew/bin/mvn package -f MavenJava'
            }
        }
    }
}
