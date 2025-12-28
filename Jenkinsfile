pipeline {
    agent { label 'TomcatServer' }

    tools {
        maven 'mvn3.9.12'
    }

    stages {

        stage('GitPull') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sharad-Chandra/FedExProjectMar13.git'
            }
        }

        stage('Build using Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Code Quality Check by SonarQube') {
            steps {
                withSonarQubeEnv('SonarQubeURL') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['TomcatServer']) {
                    echo 'Deploying WAR to Tomcat'
                    sh 'cp target/shopping-site-web-app.war /home/ubuntu/apache-tomcat-9.0.113/webapps/'
                }
            }
        }
    }
}
