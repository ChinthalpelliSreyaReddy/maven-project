pipeline {
    agent {
        label 'Dev1'
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
                    sh 'mvn clean install'
                }
            }

            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
