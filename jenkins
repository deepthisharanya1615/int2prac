pipeline {
    agent none   // No global agent — each stage defines its own agent

    stages {

        stage('Run on Controller') {
            agent { label 'built-in' }   // Runs on Jenkins controller
            steps {
                echo "Running on: ${env.NODE_NAME}" // Prints node name
            }
        }

        stage('Run on Windows Agent') {
            agent { label 'intprac' }   // Runs on agent with label "intprac"
            steps {
                bat """
                    echo Running on Windows Agent
                    javac -d out HelloWorld.java
                    java -cp out HelloWorld
                """
            }
        }

        stage('Run in Parallel') {
            parallel {
                stage('Controller') {
                    agent { label 'built-in' }
                    steps {
                        echo "Parallel on Controller: ${env.NODE_NAME}"
                    }
                }
                stage('Windows Agent') {
                    agent { label 'intprac' }
                    steps {
                        bat "echo Parallel on Windows Agent: %NODE_NAME%"
                    }
                }
            }
        }
    }
}
