pipeline {
    agent {
        label 'Dev1'
    }

    parameters {
        choice choices: ['dev', 'prod'], name: 'select_Environment'
    }

    environment {
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
                    agent { label 'Dev1' }
                    steps {
                        echo "I am from build a"
                        sh "mvn test"
                    }
                }
                stage('build b') {
                    agent { label 'Dev1' }
                    steps {
                        echo "I am from build b"
                        sh "mvn test"
                    }
                }
            }
        }

        stage('deploy_dev') {
            when {
            beforeAgent true
            expression {
                params.select_Environment == 'dev'
    }
}

            agent { label 'Dev1' }
            steps {
                dir("/var/www/html") {
                    unstash "maven-build"
                }
                sh """
                cd /var/www/html
                jar -xvf webapp.war
                """
            }
        }
    }

    post {
        success {
            dir("webapp/target/") {
                stash name: "maven-build", includes: "*.war"
            }
        }
    }
}
