pipeline {
    agent any

    options {
        timestamps()
        buildDiscarder logRotator(daysToKeepStr: '7', numToKeepStr: '10')
         // This is required if you want to clean before build
        skipDefaultCheckout(true)
    }
    
    environment {
        GIT_SECRET_CREDENTIALS = credentials('771bcedc-0fd3-421a-921f-be0033489238')
    }
    
    stages {  
                          
        stage('Checkout') {
            steps {
                script {
                    currentRevision = checkout([
                        $class: 'GitSCM', 
                        branches: [[name: '*/main']], 
                        extensions: [], 
                        userRemoteConfigs: [[
                            credentialsId: GIT_SECRET_CREDENTIALS, 
                            url: 'https://github.com/GeriCaka/Jenkins_ReadRepo.git'
                        ]]
                    ])
                }
            }
        }
        
        stage('Cred') {
            steps{
                withCredentials([file(credentialsId: 'GCPKEY', variable: 'variableName')]) {
                    echo "My secret text is ${variableName}"
                }
            }
        }

        stage('Build') {
            steps {
                // Clean before build
                cleanWs()                
                echo "Building ${env.JOB_NAME}..."
            }
        }
        
        stage('Print') {
            steps {
                echo "Current Revision ${currentRevision}"
            }
        }
    }    
}
