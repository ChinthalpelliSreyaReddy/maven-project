pipeline{

agent {
  label 'Dev1'
}
tools {
  maven 'mymaven'
}

stages{
    stage('BUILD'){
        steps{
            
           // checkout scm  // 👈 This line actually clones your repo
            //sh 'ls -la'
            sh 'mvn clean install'
        }
        post {
        success {
           archiveArtifacts artifacts: '**/target/*.war'
               }
           }

    }

    
}




}