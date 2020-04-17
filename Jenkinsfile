
node {  
    stage('Setup') {
      checkout scm
       echo "Azzuuuul... seg DevBranch"
    }

    stage("Deploying Netflix"){
        sh 'kubectl apply -f myweb.yaml'
    }

    stage("buil-heming..."){
        git url: 'git://github.com/wardviaene/kubernetes-course.git', branch: 'master'
        sh '''
          HELM_BUCKET=dev.isura-helm-repo
          PACKAGE=demo-chart
          export AWS_REGION=us-east-1
         
          helm repo add my-charts s3://${HELM_BUCKET}/charts
          cd helm/${PACKAGE}
          helm dependency update
          helm package .
          helm s3 push --force ${PACKAGE}-*.tgz my-charts
        '''
    }

}
