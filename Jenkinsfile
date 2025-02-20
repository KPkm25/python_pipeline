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
                    // Activate the virtual environment
                    sh 'source venv/bin/activate'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Activate the virtual environment and install dependencies
                    sh '''
                        source venv/bin/activate
                        pip install -r requirements.txt
                    '''
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    // Activate the virtual environment and run tests
                    sh '''
                        source venv/bin/activate
                        pytest tests/
                    '''
                }
            }
        }
        stage('Build Artifact') {
            steps {
                script {
                    // Activate the virtual environment and build the artifact
                    sh '''
                        source venv/bin/activate
                        python setup.py sdist
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
