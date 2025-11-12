pipeline {

    agent any

    environment {
        PYTHON_ENV = 'venv'
    }

    stages {

        stage('Checkout Repo') {
            steps {
                echo " Checking out repository..."
                git branch: 'main', url: 'https://github.com/Ritesh-Dhumne-incredo/Pycharm-Jenkins.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                bat '''
                    echo =======================================
                    echo Setting up Python Virtual Environment
                    echo =======================================

                    python -m venv %PYTHON_ENV%
                    call %PYTHON_ENV%\\Scripts\\activate
                    python -m pip install --upgrade pip

                    echo Python environment ready.
                '''
            }
        }

        stage('Run Python Script') {
            steps {
                bat '''
                    echo =======================================
                    echo Running Python Script via Jenkins
                    echo =======================================

                    if not exist test_script (
                        echo File test_script not found!
                        exit /b 1
                    )

                    call %PYTHON_ENV%\\Scripts\\activate
                    python test_script

                    if %errorlevel% neq 0 (
                        echo Python script failed with exit code %errorlevel%
                        exit /b %errorlevel%
                    ) else (
                        echo Python script executed successfully!
                    )
                '''
            }
        }
    }

    post {
        always {
            echo "Jenkins pipeline finished."
        }
        success {
            echo "Python script ran successfully — pipeline passed!"
        }
        failure {
            echo "Jenkins pipeline failed — check logs for details."
        }
    }
}
