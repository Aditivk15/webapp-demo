pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME' // Define in Jenkins → Manage Jenkins → Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/your-username/webapp-demo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project with Maven...'
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo 'Deploying WAR file to Tomcat...'
                deploy adapters: [tomcat9(
                    credentialsId: 'tomcat-credentials',
                    path: '',
                    url: 'http://localhost:8081'
                )], contextPath: 'webapp-demo', war: '**/target/*.war'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
