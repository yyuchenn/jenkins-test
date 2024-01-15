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
            parallel {
                stage('Build Manager') {
                    steps {
                        sh """
                            export GOPATH=\$HOME/go
                            export PATH=\$PATH:/usr/local/go/bin
                            go build -o taget/manager multi-node/manager
                        """   
                    }
                }

                stage('Build Worker') {
                    steps {
                        sh """
                            export GOPATH=\$HOME/go
                            export PATH=\$PATH:/usr/local/go/bin
                            go build -o taget/worker multi-node/worker
                        """   
                    }
                }
            }
            
        }
    }
}
