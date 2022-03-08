
pipeline {
    agent any
    stages {
        stage('Parameters'){
            steps {
                script {
                    properties([
                        parameters([
                            [$class: 'ChoiceParameter', 
                                choiceType: 'PT_SINGLE_SELECT', 
                                description: 'Microservice Project Name', 
                                filterLength: 1, 
                                filterable: true, 
                                name: 'MICROSERVICE_NAME', 
                                script: [
                                    $class: 'GroovyScript', 
                                    fallbackScript: [
                                        classpath: [], 
                                        sandbox: false, 
                                        script: 
                                            "return ['ERROR']"
                                    ], 
                                    script: [
                                        classpath: [], 
                                        sandbox: false, 
                                        script: 
                                            "return['dev','stage','prod']"
                                    ]
                                ]
                            ]                               
                        ])
                    ])
                }
            }
        }
    }   
}
