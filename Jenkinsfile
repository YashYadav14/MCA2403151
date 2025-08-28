pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "=== Build Stage ==="
                // Dummy build command (safe, no pom.xml needed)
                sh 'echo "Simulating: mvn clean package"'
            }
        }

        stage('Test') {
            steps {
                echo "=== Test Stage ==="
                // Dummy test command (safe)
                sh 'echo "Simulating: mvn test"'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "=== Deploy Stage ==="
                // Dummy deploy step
                sh 'echo "Deploying on main branch..."'
            }
        }
    }

    post {
        always {
            echo "Pipeline finished. BUILD_NUMBER=${env.BUILD_NUMBER}, BRANCH=${env.BRANCH_NAME}"
        }
    }
}
