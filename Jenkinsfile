pipeline {
    agent {
        label 'slave1'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/manuraj-1996/Devops.git',
                        credentialsId: 'New'
                    ]]
                ])
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
    steps {
        // This wrapper provides the environment for configFile
        configFileProvider([configFile(fileId: 'my-maven-settings', variable: 'MAVEN_SETTINGS')]) {
            sh "mvn deploy -s $MAVEN_SETTINGS"
        }
    }
}
    }
}

