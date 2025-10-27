pipeline {
    agent any

    tools {
         maven 'Maven 3.9.11' // Define in Jenkins → Manage Jenkins → Global Tool Configuration
    }


     stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-token',   // <-- Set your GitHub token ID here
                    url: 'https://github.com/Aditivk15/webapp-demo.git'
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
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-credentials',
                        path: '',
                        url: 'http://localhost:8080'
                    )
                ],
                contextPath: 'webapp-demo',
                war: '**/target/*.war'
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
