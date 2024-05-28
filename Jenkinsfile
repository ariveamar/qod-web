pipeline {
    agent any

    stages {
        stage("Checkout") {
            steps {
                checkout scm
            }
        }
        stage("Docker Build") {
            steps {
              sh '''
                  #oc start-build --from-build=<build_name>
                  oc start-build  -F qod-web --from-dir=./deployment/buildconfig.yaml
              '''
            }
        }
        stage("Create Deployment") {
            steps {
              sh '''
                  oc apply -f ./deployment/deployment.yaml
              '''
            }
        }
        stage("Create Service") {
            steps {
              sh '''
                  oc apply -f ./deployment/service.yaml
              '''
            }
        }
        stage("Expose Route") {
            steps {
              sh '''
                  oc apply -f ./deployment/route.yaml
              '''
            }
        }
    }
