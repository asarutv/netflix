
node {  
    stage('Setup') {
      checkout scm
       echo "Azzuuuul... seg DevBranch"
    }

    stage("Deploying Netflix"){
        sh 'kubectl apply -f myweb.yaml'
    }

    stage("buil-heming..."){
        
        sh '''
          HELM_BUCKET=dev.isura-helm-repo
          PACKAGE=1.ms-browse
         
          helm repo add my-charts s3://${HELM_BUCKET}/charts 
          
          helm package ${PACKAGE}

          helm s3 push --force ${PACKAGE}-*.tgz my-charts
        '''
    }

}
