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
                    export GOPATH=/usr/local/go
                    export PATH=\$PATH:\$GOPATH/bin
                    go build -o taget/manager manager  
                """   
            }
        }
    }
}
