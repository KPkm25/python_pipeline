pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git url:'https://github.com/KPkm25/python_pipeline.git', branch:'main'
            }
        }
        stage('Set up Virtual Environment') {
            steps {
                script {
                    // Create a virtual environment
                    sh 'python3 -m venv venv'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Use the pip from the virtual environment to install dependencies
                    sh '''
                        source venv/bin/activate
                        venv/bin/pip install -r requirements.txt
                    '''
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    // Use the python and pip from the virtual environment
                    sh '''
                        source venv/bin/activate
                        venv/bin/pytest tests/
                    '''
                }
            }
        }
        stage('Build Artifact') {
            steps {
                script {
                    // Use python from the virtual environment to build the artifact
                    sh '''
                        source venv/bin/activate
                        venv/bin/python setup.py sdist
                    '''
                }
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'dist/*.tar.gz', fingerprint: true
            }
        }
    }
}
