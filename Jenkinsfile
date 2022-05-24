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
                             sh  ' oc create deployment  webapp   --image quay.io/mayank123modi/mayanknginximage'
                        }
                    }
                }
            }
        }

        stage('stage 2') {
            steps {
                echo" creating the svc"
             sh  ' oc expose deployment webapp  --port 80'
            }
        }


        stage('stage 3') {
            steps {
                echo "creating the route"
               sh ' oc expose service  webapp'
            }
        }

    }
}
