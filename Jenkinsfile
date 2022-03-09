pipeline {
    agent any

    options {
        timestamps()
        buildDiscarder logRotator(daysToKeepStr: '7', numToKeepStr: '10')
         // This is required if you want to clean before build
        skipDefaultCheckout(true)
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
                            credentialsId: 'f7df551d-63c9-4ebd-80ad-13e602b795c5', 
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
