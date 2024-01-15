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
                sh 'echo "BOEING 737"'

            }
        }
        stage('Run') {
            steps {
                sh 'python3 adder.py 3 5'
                sh 'echo "I CAN DO WHATEVER I IMAGINE, JUST BELIEVE!"'
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
    }
    post {
        always {
            junit 'junit.xml'
            cobertura coberturaReportFile: 'coverage.xml'
        }
    }
}