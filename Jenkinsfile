pipeline {
    agent {
        dockerfile {
            label 'docker'
        }
    }
    stages {
        stage('Compile') {
            steps {
                sh 'python3 -m compileall adder.py'
                sh 'echo "BOEING 747-800"'

            }
        }
        stage('Run') {
            steps {
                sh 'python3 adder.py 3 5'
                sh 'echo "Boeing 737Max"'
            }
        }
        stage('Unit test') {
            steps {
                sh '''python3 -m pytest \
                    -v --junitxml=junit.xml \
                    --cov-report xml --cov adder adder.py
                '''
            }
        }
        stage('After unit test') {
            steps {
                sh 'echo "After unit test!"'
            }
        }
        stage('Build Deploy Code') {
            when {
                branch 'main'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }
    }
    post {
        always {
            junit 'junit.xml'
            cobertura coberturaReportFile: 'coverage.xml'
        }
    }
}
