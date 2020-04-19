
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
          PACKAGE=ms-browse
         
          helm repo add my-charts s3://${HELM_BUCKET}/charts 
          
          helm package ${PACKAGE}

          helm s3 push --force ${PACKAGE}-*.tgz my-charts

         cd /var/lib/jenkins/workspace/pipeline-k8s/ 
         rm -rf ${PACKAGE}-*.tgz 
        '''
    }

    stage("Deploying with helm"){
          sh '''
            HELM_BUCKET=dev.isura-helm-repo
            PACKAGE=ms-browse
            NS=front-01
            NSV=$(kubectl get ns |grep -E "${NS}" |wc -l)
               if [ $NSV -eq 1 ] 
                    then
                        echo "${NS} already exist"
                    else
                        kubectl create ns ${NS}
                fi
            
            kubectl config set-context k8s.dev.isura.club --namespace=front-01
            helm repo add my-charts s3://${HELM_BUCKET}/charts
          
            DEPLOYED=$(helm list |grep -E "${PACKAGE}" |grep deployed |wc -l)
              if [ $DEPLOYED -eq 0 ]
                then
                    helm install ${PACKAGE} my-charts/${PACKAGE}
                else
                    helm upgrade ${PACKAGE} my-charts/${PACKAGE}
              fi
            echo "deployed!"
            kubectl config set-context k8s.dev.isura.club --namespace=default
          '''
    }

}
