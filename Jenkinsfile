def executeScript(stageName) {
    executeScript(stageName, 10)
}

def executeScript(stageName, max) {
    for (int i = 1; i <= max; ++i) {
        echo "This is branch ${stageName} => ${i}/${max}"
        sh """
                        #!/bin/bash
                        if [[ "${stageName}" == *Fail ]] || [ "\$(( RANDOM % 100 ))x" = "1x" ]; then
                        echo "something failed";
                        exit 1
                        fi
                        #sleep 1
                        """
    }
}

pipeline {
    agent {kubernetes {}}
    stages {
        stage('Generate JUnit results') {
            steps {
                mockLoad 20
                junit 'mock-junit.xml'
            }
        }
        stage('Trigger Related Build')
        {
            steps{
                build wait: false, propagate: false, job: 'hello'
            }
        }
        stage('Create Artifact')
        {
            steps{
                sh 'touch artifact.txt'
                archiveArtifacts 'artifact.txt'
            }
        }
        stage('Skipped Stage 1') {
            when {
                branch 'unknown'
            }
            steps {
                echo 'Skipped step.'
            }
        }
        stage('Parallel Stage') {
            parallel {
                stage('Branch A') {
                    steps {
                        executeScript('Branch A')
                    }
                }
                stage('Branch B') {
                    stages {
                        stage('Nested B1') {
                            steps {
                                script {
                                    executeScript('Nested B1 within Branch B')
                                }
                            }
                        }
                        stage('Nested B2') {
                            steps {
                                executeScript('Nested B2 within Branch B Fail')
                            }
                        }
                    }
                }
                stage('Branch C') {
                    stages {
                        stage('Nested C1') {
                            steps {
                                executeScript('Nested C1 within Branch C')
                            }
                        }
                        stage('Nested C2') {
                            stages {
                                stage('Nested C21') {
                                    steps {
                                        executeScript('Nested C21 within Branch C')
                                    }
                                }
                                stage('Nested C22') {
                                    steps {
                                        executeScript('Nested C22 within Branch C Fail')
                                    }
                                }
                                stage('Nested C23') {
                                    steps {
                                        executeScript('Nested C23 within Branch C Fail')
                                    }
                                }
                            }
                        }
                    }
                }
                stage('Skipped Parallel') {
                    when {
                        branch 'unknown'
                    }
                    steps {
                        echo 'Skipped step.'
                    }
                }
                stage('🏃 Branch D 🏃') {
                    stages {
                        stage('Nested D1') {
                            steps {
                                executeScript('Nested D1 within Branch D')
                            }
                        }
                        stage('Nested D2') {
                            stages {
                                stage('Nested D21') {
                                    steps {
                                        executeScript('Nested D21 within Branch D')
                                    }
                                }
                                stage('Nested D22') {
                                    steps {
                                        executeScript('Nested D22 within Branch D')
                                    }
                                }
                                stage('Nested D23') {
                                    steps {
                                        sh """
                                            #!/bin/bash
                                            echo generic > error.txt
                                            cat error.txt
                                            ls -fail
                                        """
                                    }
                                }
                            }
                        }
                        stage('Nested D3') {
                            stages {
                                stage('Nested D31') {
                                    steps {
                                        executeScript('Nested D31 within Branch D')
                                    }
                                }
                                stage('Nested D32') {
                                    stages {
                                        stage('Nested D321') {
                                            steps {
                                                executeScript('Nested D321 within Branch D')
                                            }
                                        }
                                        stage('Nested D322') {
                                            steps {
                                                executeScript('Nested D322 within Branch D')
                                            }
                                        }
                                        stage('Nested D323') {
                                            steps {
                                                executeScript('Nested D323 within Branch D')
                                            }
                                        }
                                        stage('Nested D324') {
                                            steps {
                                                executeScript('Nested D324 within Branch D')
                                            }
                                        }
                                        stage('Nested D325') {
                                            steps {
                                                executeScript('Nested D325 within Branch D')
                                            }
                                        }
                                        stage('Nested D326') {
                                            steps {
                                                executeScript('Nested D326 within Branch D')
                                            }
                                        }
                                        stage('Nested D327') {
                                            steps {
                                                executeScript('Nested D327 within Branch D')
                                            }
                                        }
                                        stage('Nested D328') {
                                            steps {
                                                executeScript('Nested D328 within Branch D')
                                            }
                                        }
                                        stage('Nested D329') {
                                            steps {
                                                executeScript('Nested D329 within Branch D')
                                            }
                                        }
                                        stage('Nested D32A') {
                                            steps {
                                                executeScript('Nested D32A within Branch D')
                                            }
                                        }
                                        stage('Nested D32B') {
                                            steps {
                                                executeScript('Nested D32B within Branch D')
                                            }
                                        }
                                        stage('Nested D32C') {
                                            steps {
                                                executeScript('Nested D32C within Branch D Fail')
                                            }
                                        }
                                        stage('Nested D32D') {
                                            steps {
                                                executeScript('Nested D32D within Branch D Fail')
                                            }
                                        }
                                        stage('Nested D32E') {
                                            steps {
                                                executeScript('Nested D32E within Branch D Fail')
                                            }
                                        }
                                        stage('Nested D32F') {
                                            steps {
                                                executeScript('Nested D32F within Branch D Fail')
                                            }
                                        }
                                        stage('Nested D32G') {
                                            steps {
                                                executeScript('Nested D32G within Branch D')
                                            }
                                        }
                                        stage('Nested D32H') {
                                            steps {
                                                executeScript('Nested D32H within Branch D')
                                            }
                                        }
                                        stage('Nested D32I') {
                                            steps {
                                                executeScript('Nested D32I within Branch D')
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    }
                }
                stage('Skipped E') {
                    steps {
                        executeScript('Skipped E')
                    }
                }
            }
        }
        stage('Skipped Stage 2') {
            steps {
                executeScript('Skipped Stage 2')
            }
        }
        stage('Skipped Stage 3') {
            steps {
                executeScript('Skipped Stage 3')
            }
        }
    }
}
