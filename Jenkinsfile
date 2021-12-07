pipeline {
  agent any
  stages {
    stage('Build & Push to ECR') {
      parallel {
        stage('Build & Push to ECR') {
          steps {
            dir(path: 'source/calculation-offer-service/CalculationServiceAPISolution') {
              sh 'pwd'
              sh 'docker build -t $CALCULATION_SERVICE_IMAGE:latest -t $CALCULATION_SERVICE_IMAGE:$BUILD_NUMBER .'
              sh 'docker tag $CALCULATION_SERVICE_IMAGE:latest $ECR_ID/$CALCULATION_SERVICE_IMAGE:latest'
              sh 'docker tag $CALCULATION_SERVICE_IMAGE:$BUILD_NUMBER $ECR_ID/$CALCULATION_SERVICE_IMAGE:$BUILD_NUMBER'
              sh 'docker login --username $ECR_CREDENTIALS_USR --password $ECR_CREDENTIALS_PSW $ECR_ID'
              sh 'docker image prune -f'
              sh 'docker push $ECR_ID/$CALCULATION_SERVICE_IMAGE:latest'
            }

          }
        }

        stage('Identity_Verification_Response_Deamon') {
          steps {
            dir(path: 'source/creditcard-identity-verification-response-daemon') {
              sh 'pwd'
              sh 'docker build -t $IDENTITY_VERIFICATION_RESPONSE_DEAMON -t $IDENTITY_VERIFICATION_RESPONSE_DEAMON:$BUILD_NUMBER .'
              sh 'docker tag $IDENTITY_VERIFICATION_RESPONSE_DEAMON $ECR_ID/$IDENTITY_VERIFICATION_RESPONSE_DEAMON'
              sh 'docker tag $IDENTITY_VERIFICATION_RESPONSE_DEAMON:$BUILD_NUMBER $ECR_ID/$IDENTITY_VERIFICATION_RESPONSE_DEAMON:$BUILD_NUMBER'
              sh 'docker login --username $ECR_CREDENTIALS_USR --password $ECR_CREDENTIALS_PSW $ECR_ID'
              sh 'docker image prune -f'
              sh 'docker push $ECR_ID/$IDENTITY_VERIFICATION_RESPONSE_DEAMON:latest'
            }

          }
        }

      }
    }

  }
  environment {
    ECR_ID = '142198642907.dkr.ecr.us-west-1.amazonaws.com'
    CALCULATION_SERVICE_IMAGE = 'karthickv2-casestudy-calculation-service'
    ECR_CREDENTIALS = credentials('ecr-credentials')
  }
}