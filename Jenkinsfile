pipeline {
    agent {
        label 'label_1'
    }

    tools {
        go '1.19'
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
                            go build -o taget/manager multi-node/manager
                        """   
                    }
                }

                stage('Build Worker') {
                    steps {
                        sh """
                            go build -o taget/worker multi-node/worker
                        """   
                    }
                }
            }
            
        }
    }
}
