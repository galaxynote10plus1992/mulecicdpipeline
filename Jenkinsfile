pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('anypoint.credentials	')
    MULE_VERSION = '4.3.0'
    WORKER = "MICRO"
  }
  stages {
    stage('Build') {
      steps {
             bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
         bat "mvn test"
      }
    }

     stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'DEV'
        APP_NAME = 'mulecicdpipeline'
      }
      steps {
            bat 'mvn clean package deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Dusername="%DEPLOY_CREDS_USR%" -Dpassword="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
      }
    }

  }
  
  tools {
    maven 'MAVEN_HOME'
  }

 
}