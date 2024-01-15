pipeline {
    agent {
        label 'label_1'
    }
    stages {
        stage('Pull') {
            steps {
                echo 'Hello world!'
                git branch: 'main', credentialsId: 'yuchenGithub', url: 'git@github.com:yyuchenn/multi-node.git'
            }
        }
        stage('Build') {
            steps {
                sh """
                    export PATH=\$PATH:/usr/local/go/bin
                    go build -o taget/manager manager  
                """   
            }
        }
    }
}
