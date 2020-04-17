
node {  
    stage('Setup') {
      checkout scm
       echo "Azzuuuul... seg DevBranch
    }

    stage("Deploying Netflix"){
        sh 'kubectl apply -f myweb.yaml'
    }

}
