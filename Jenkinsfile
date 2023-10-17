pipeline {
  agent { label 'workstation' }

   options {
     ansiColor('xterm')
   }

  stages {

    stage('Download Dependencies'){
      steps {
        sh 'npm install'
        sh 'env'
      }
    }

    stage('Code Quality'){
      when {
        allOf {
        expression { env.TAG_NAME != env.GIT_BRANCH }
        }
      }
      steps {
        //sh 'sonar-scanner -Dsonar.host.url=http://172.31.41.26:9000 -Dsonar.login=admin -Dsonar.password=admin123 -Dsonar.projectKey=backend -Dsonar.qualitygate.wait=true'
        echo 'OK'
      }
    }

    stage('Unit Tests'){
      when {
        allOf {
        expression { env.TAG_NAME != env.GIT_BRANCH }
        branch 'main'
        }
      }
      steps {
      // Ideally we should run Unit Test , but in this practice we skipped it. Below is the command to run the unit test
      // sh 'npm test'
        echo 'CI'
      }
    }

    stage('Release') {
      when {
        expression { env.TAG_NAME ==~ ".*" }
      }
      steps {
        sh 'zip -r backend-${TAG_NAME}.zip node_modules schema DbConfig.js index.js package.json TransactionService.js'
      }
    }

  }
}
//