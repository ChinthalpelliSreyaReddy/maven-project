pipeline {
    agent {
        label 'Dev1'
    }

parameters {
  choice choices: ['dev', 'prod'], name: 'select_Environment'
}

environment{
    NAME = "Sreya"
}
    tools {
        maven 'mymaven'
    }

    stages {
        stage('BUILD') {
            steps {
                checkout scm
                sh 'ls -la'

                withEnv(["JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64", "PATH=/usr/lib/jvm/java-17-openjdk-amd64/bin:$PATH"]) {
                    sh 'java -version'
                    sh 'mvn clean install --settings ./settings.xml -DskipTests=true'
                    echo " hello $NAME ${params.LASTNAME}"
                }
            }

           
        }
      stage('test') {
    parallel {
        stage('build a') {
            steps {
                echo "I am from build a"
                sh "mvn test"
            }
        }
        stage('build b') {
            steps {
                echo "I am from build b"
                sh "mvn test"
            }
        }
    }
}

}
         post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        
    
}
