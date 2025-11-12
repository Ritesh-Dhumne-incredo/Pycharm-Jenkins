pipeline {

    agent any
 
    environment {

        PYTHON_ENV = 'venv'

    }
 
    stages {
 
        stage('Checkout Repo') {

            steps {

                git branch: 'main', url: 'https://github.com/Hritik-Incredo/SStream.git'

            }

        }
 
        stage('Setup Python Environment') {

            steps {

                bat '''

                python -m venv %PYTHON_ENV%

                call %PYTHON_ENV%\\Scripts\\activate

                python -m pip install --upgrade pip

                '''

            }

        }
 
        stage('Run Python Script') {

            steps {

                bat '''

                call %PYTHON_ENV%\\Scripts\\activate

                python test_script.py

                '''

            }

        }

    }
 
    post {

        always {

            echo "🧾 Jenkins pipeline finished."

        }

        success {

            echo "✅ Python script ran successfully!"

        }

        failure {

            echo "❌ Jenkins pipeline failed."

        }

    }

}

 
