pipeline {
    agent { label 'AGENT-1' }
    environment { 
        PROJECT = 'expense'
        COMPONENT = 'backend'
        appVersion = ''
      
    }
    options {
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }
    // parameters{
    //     booleanParam(name: 'deploy', defaultValue: false, description: 'Toggle this value')
    // }
    stages {
        stage('Read Version') {
            steps {
               script{
                 def packageJson = readJSON file: 'package.json'
                 appVersion = packageJson.version
                 echo "Version is: $appVersion"
               }
            }
        }
        stage('Install Dependencies') {
            steps {
               script{ 
                 sh """
                    npm install
                 """
               }
            }
        }
        
        stage('Docker Build') {
            steps {
               script{
               sh """
                    docker build -t backend:v1.0.0. .
                 """
               }
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure { 
            echo 'I will run when pipeline is faile okay'
        }
        success { 
            echo 'I will run when pipeline is success'
        }
    }
}