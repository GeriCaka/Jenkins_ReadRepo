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
        SECRET_FILE_JSON = credentials('GCPKEY')
    }
    
    stages {       
        

        
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
                // We need to explicitly checkout from SCM here
                script {
                    currentRevision = checkout([
                            $class: 'GitSCM', 
                            branches: [[name: '*/main']],                              
                            userRemoteConfigs: [[
                                credentialsId: "771bcedc-0fd3-421a-921f-be0033489238", 
                                url: 'https://github.com/GeriCaka/Jenkins_ReadRepo.git'
                            ]]
                    ])
                }
                echo "Building ${env.JOB_NAME}..."
                echo "----------- My secret file json is ${SECRET_FILE_JSON}"
                bat """
                echo "Holaaa ${currentRevision}"
                cd src 
                :This is a comment in sh & I am changing the directory to myFolder
                """
            }
        }
        
        stage('Print') {
            steps {
                echo "Current Revision ${currentRevision}"
            }
        }
    }    
}
