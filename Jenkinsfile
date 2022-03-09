pipeline {
    agent any
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
            
            stage('Print') {
                steps {
                    echo "Current Revision ${currentRevision}"
                }
            }
        }    
}
