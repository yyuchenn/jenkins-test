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

        post {
            success {
                stage('Run') {
                    parallel {
                        stage('Run Manager') {
                            steps {
                                sh 'target/manager :80 :1234 1 :1235 2 :1236'
                            }
                        }
                        
                        stage('Run Worker 1') {
                            steps {
                                sleep(time:2,unit:"SECONDS")
                                sh 'target/worker 1 :1234 :1235'
                            }
                        }

                        stage('Run Worker 2') {
                            steps {
                                sleep(time:2,unit:"SECONDS")
                                sh 'target/worker 2 :1234 :1236'
                            }
                        }
                    }
                }
            }
        }
    }
}
