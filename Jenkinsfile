pipeline{
  agent any
  stages{
    stage ('Build'){
    steps {
      sh'mvn clean package'
    }
    post {
      success{
        echo "Archiving..."
        archiveArtifacts artifacts:'**/target/*.war'
      }
    }
   }
  stage ('Deploy to staging'){
    steps{
      build job:'Deploy app'
    }
  }
  stage ('Deploy to prod'){
    steps{
      timeout(time:5,unit:'DAYS'){
        input message:'Approve Prod deployment?'
      }
      build job:'Deploy to prod'
    }
  }
 }
}