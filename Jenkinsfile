pipeline {
  agent any 
  
  triggers {
    pollSCM '* * * * *'
  }
  
  stages {
    stage('Calling Base!'){
      steps { 
        echo "${env.WORKSPACE}"
        echo 'Calling Base'
        build job: 'git_base',
              parameters: [
                booleanParam(name: 'StageA', value: "false"),
                booleanParam(name: 'StageB', value: "false"),
                booleanParam(name: 'StageC', value: "false"),
                booleanParam(name: 'Build', value: "false"),
                string(name: 'Workspace', value: "${env.WORKSPACE}")
              ],
              wait: true, 
              propagate: true
      }      
    }
    
    stage('CustomStage') {
      steps {
        echo 'CustomStage'
      }
    }   
  }
}
