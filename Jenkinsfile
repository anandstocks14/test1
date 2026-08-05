pipeline {
    agent none

    stages {

        stage('Checkout') {
            agent { label 'built-in' }   // or 'master'
            steps {
                git branch: 'main',
                    url: 'https://github.com/anandstocks14/project1.git'
            }
        }

        stage('Build') {
            agent { label 'built-in' }   // or 'master'
            steps {
                dir('sample-app') {
                    sh 'mvn clean package'
                    stash name: 'war', includes: 'target/sample.war'
                }
            }
        }

        stage('Deploy') {
            agent { label 'my-worker' }
            steps {
                unstash 'war'
                sh '''
                sudo cp target/sample.war /opt/tomcat/webapps/sample.war
                '''
            }
        }
    }
}
