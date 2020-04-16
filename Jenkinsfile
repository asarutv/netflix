
node {  
    stage('Setup') {
      checkout scm
       echo "Azzuuuul... "
    }

    stage("Deploying Netflix"){
        sh 'kubectl apply -f myweb.yaml'
    }

}
