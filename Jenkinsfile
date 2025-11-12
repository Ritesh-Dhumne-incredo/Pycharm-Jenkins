pipeline {

    agent any

    environment {
        PYTHON_ENV = 'venv'
        SCRIPT_PATH = 'test_script.py'
    }

    stages {

        stage('Checkout Repo') {
            steps {
                echo "🧾 Checking out repository..."
                git branch: 'main', url: 'https://github.com/Hritik-Incredo/SStream.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                bat '''
                    echo ==============================
                    echo Creating and Activating Python venv
                    echo ==============================

                    python -m venv %PYTHON_ENV%
                    call %PYTHON_ENV%\\Scripts\\activate
                    python -m pip install --upgrade pip

                    echo ✅ Virtual environment ready.
                '''
            }
        }

        stage('Run Python Script') {
            steps {
                bat '''
                    echo ==============================
                    echo Running Python Script
                    echo ==============================

                    call %PYTHON_ENV%\\Scripts\\activate

                    if not exist "%SCRIPT_PATH%" (
                        echo ❌ File %SCRIPT_PATH% not found!
                        dir
                        exit /b 1
                    )

                    python "%SCRIPT_PATH%"
                    if %ERRORLEVEL% NEQ 0 (
                        echo ❌ Python script failed with exit code %ERRORLEVEL%
                        exit /b %ERRORLEVEL%
                    ) else (
                        echo ✅ Python script ran successfully!
                    )
                '''
            }
        }

    }

    post {
        always {
            echo "🧾 Jenkins pipeline finished."
        }
        success {
            echo "✅ Python script executed successfully!"
        }
        failure {
            echo "❌ Python script failed — check above logs."
        }
    }

}
