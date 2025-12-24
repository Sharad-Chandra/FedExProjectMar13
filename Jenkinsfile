pipeline {
    agent { label 'TomcatServer' }  // correct

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

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('Deploy') {
            steps {
                sshagent(['TomcatServer']) {
                    echo 'Deploying WAR to Tomcat'
                    // Stop Tomcat
                    //sh '/home/ubuntu/apache-tomcat-9.0.113/bin/shutdown.sh || true'
                    // Copy WAR to Tomcat webapps folder
                    sh 'cp target/shopping-site-web-app.war /home/ubuntu/apache-tomcat-9.0.113/webapps/'
                    // Start Tomcat
                    //sh '/home/ubuntu/apache-tomcat-9.0.113/bin/startup.sh'
                }
            }
        }
    }
}
