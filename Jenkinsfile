pipeline{

agent none

stages{
    stage('BUILD'){
        steps{
            echo "this is my first pipeline demo"
            checkout scm  // 👈 This line actually clones your repo
            sh 'ls -la'
        }
    }

    stage('DEV'){
        steps{
            echo "this is dev repos"
        }
    }
    stage('prod'){
        steps{
            echo "this is prod rep"
        }

    }
}


}