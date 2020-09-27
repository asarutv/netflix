


HELM_CHART = "nodejs-chart"
IMAGE_TAG = "0.1.$BUILD_ID"
IMAGE_NAME="harbor.asaru.info\\/public-01\\/\$JOB_NAME"
REPO_NAME="harbor.asaru.info\\/public-01\\/$JOB_NAME"
IMAGE_REPO = "harbor.asaru.info/public-01/$JOB_NAME"
MS_NAME="$JOB_NAME"

pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      yaml """
kind: Pod
metadata:
  name: kaniko
spec:
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug-539ddefcae3fd6b411a95982a830d987f4214251
    imagePullPolicy: Always
    command:
    - cat
    tty: true
    volumeMounts:
      - name: docker-config
        mountPath: /kaniko/.docker
  volumes:
    - name: docker-config
      configMap:
        name: docker-config
"""
    }
  }
  stages {
    stage('Build with Kaniko') {
      steps {
        checkout scm
        container(name: 'kaniko') {
            sh """
               ls
               /kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --no-push
               ls
            """
        }
      }
    }
  }
}

