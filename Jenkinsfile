pipeline {
    options {
        // set a timeout of 30 minutes for this pipeline
        timeout(time: 30, unit: 'MINUTES')
    }
    agent {
      node {
        label 'master'
      }
    }

    stages {

        stage('stage 1') {
            steps {
                script {
                    openshift.withCluster() {
                        openshift.withProject() {
                                echo "stage 1: using project: ${openshift.project()} in cluster ${openshift.cluster()} creating the deployment"
                               " oc create deployment  webapp   --image quay.io/mayank123modi/mayanknginximage"
                        }
                    }
                }
            }
        }

        stage('stage 2') {
            steps {
                sh 'creating the svc'
               " oc expose deployment webapp  --port 80"
            }
        }


        stage('stage 3') {
            steps {
                sh 'creating the route'
               " oc expose service  webapp"
            }
        }

    }
}
