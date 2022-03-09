pipeline {
    agent any

    options {
        timestamps()
        buildDiscarder logRotator(daysToKeepStr: '7', numToKeepStr: '10')
         // This is required if you want to clean before build
        skipDefaultCheckout(true)
    }  
    environment{
        SECRET = credentials('My_secret_Text')
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
                            credentialsId: "771bcedc-0fd3-421a-921f-be0033489238", 
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
                echo "My secret text is ${env.SECRET}"
            }
        }
        
        stage('Print') {
            steps {
                echo "Current Revision ${currentRevision}"
            }
        }
    }    
}
