pipeline {
    agent {
        label 'label_1'
    }
    stages {
        stage('Pull') {
            steps {
                git branch: 'main', credentialsId: 'yuchenGithub', url: 'git@github.com:yyuchenn/multi-node.git'
            }
        }
        stage('Build') {
            steps {
                sh """
                    pwd
                    export GOPATH=\$HOME/go
                    export PATH=\$PATH:/usr/local/go/bin
                    go build -o taget/manager manager  
                """   
            }
        }
    }
}
