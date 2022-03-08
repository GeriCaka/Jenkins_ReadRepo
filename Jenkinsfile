pipeline {
    agent any
    parameters {
        activeChoiceParam('choice1') :
            description('select your choice')
            choiceType('RADIO')
            groovyScript {
                script("return['aaa','bbb']")
                fallbackScript('return ["error"]')            
            }
    }
  
    stages {
    
        stage('Hello') {
            steps {
                echo 'Hello World!'
            }      
        }
    
        stage("Build") {
            steps {
                bat "mvn clean install"
            }
        }    
    
    }
}
