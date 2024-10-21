pipeline {
       agent any
       stages {
           stage('Checkout') {
               steps {
                   checkout scm
               }
           }
           stage('Install Dependencies') {
               steps {
                   sh 'npm install' // Use 'bat' for Windows
               }
           }
           stage('Run Tests') {
               steps {
                   sh 'npm test' // Use 'bat' for Windows
               }
           }
           stage('Build') {
               steps {
                   sh 'npm run build' // Use 'bat' for Windows
               }
           }
           stage('Docker Build') {
               steps {
                   sh 'docker build -t safeeha/counter-app:latest .' // Use 'bat' for Windows
               }
           }
           stage('Docker Push') {
               steps {
                   withCredentials([string(credentialsId: 'dockerhub-credentials', variable: 'DOCKERHUB_CREDENTIALS')]) {
                       sh 'echo "$DOCKERHUB_CREDENTIALS" | docker login -u safeeha --password-stdin'
                       sh 'docker push safeeha/counter-app:latest'
                   }
               }
           }
       }
   }
