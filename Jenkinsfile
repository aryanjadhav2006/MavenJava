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

    post {
        always {
            emailext(
                to: 'aryanjadhav3344@gmail.com',
                subject: "Jenkins Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                body: """
                    <h2>Jenkins Build Notification</h2>
                    <p><b>Job:</b> ${env.JOB_NAME}</p>
                    <p><b>Build:</b> #${env.BUILD_NUMBER}</p>
                    <p><b>Status:</b> ${currentBuild.currentResult}</p>
                    <p><b>Build URL:</b> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                """,
                mimeType: 'text/html'
            )
        }
    }
}
