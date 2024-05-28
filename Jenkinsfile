pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage("Docker Build") {
            steps {
              sh '''
                  #oc start-build --from-build=<build_name>
                  oc start-build qod-web --from-dir=./deployment/buildconfig.yaml
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
}
