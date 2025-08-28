pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // make sure we have the repo checked out
        checkout scm
        echo "Checked out branch: ${env.BRANCH_NAME ?: env.GIT_BRANCH ?: 'unknown'}"
      }
    }

    stage('Build') {
      // Run this stage only on the 'development' branch
      when {
        branch 'development'
      }
      steps {
        echo "== BUILD stage (only on development) =="
        // replace the command below with your real build (mvn, gradle, npm, etc.)
        sh 'echo Building... && sleep 1'
        // e.g. sh 'mvn -DskipTests clean package'
      }
    }

    stage('Test') {
      steps {
        echo "== TEST stage (runs on all branches) =="
        // replace with your test command
        sh 'echo Running tests... && sleep 1'
        // e.g. sh 'mvn test'
      }
    }

    stage('Deploy') {
      steps {
        script {
          // Ask the user to enter the build number to deploy.
          // Default value will show the current Jenkins BUILD_NUMBER.
          def userInput = input message: 'Enter build number to deploy (leave default to use current build):',
                               parameters: [string(name: 'DEPLOY_BUILD_NUMBER', defaultValue: "${env.BUILD_NUMBER}", description: 'Build number to deploy')]

          // input returns either a string or a map; handle both
          def deployBuildNumber = (userInput instanceof Map) ? userInput['DEPLOY_BUILD_NUMBER'] : userInput

          echo "Deploying using build number: ${deployBuildNumber}"
          // Place your real deploy command below (scp, ansible, kubectl, etc.)
          sh "echo Simulating deploy of build ${deployBuildNumber} && sleep 1"
        }
      }
    }
  }

  post {
    always {
      echo "Pipeline finished. Jenkins BUILD_NUMBER = ${env.BUILD_NUMBER}"
      // optional: archive artifacts, publish test reports
      // archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
      // junit '**/target/surefire-reports/*.xml'
    }
  }
}
