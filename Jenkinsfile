node{
   
   stage("App Build started"){
      echo 'App build started..'
      git credentialsId: 'Github-ID', url: 'https://github.com/itrainspartans/python-docker-app-openshifts.git'
      }
   
   stage('Docker Build') {
     def app = docker.build "madhu-pk/py-spartans"
    }
   
   stage("Tag & Push image"){
      withDockerRegistry([credentialsId: 'dockerID',url: ""]) {
          sh 'docker tag madhu/py-spartans madhu/py-spartans:dev'
          sh 'docker push madhu/py-spartans:dev'
          sh 'docker push madhu/py-spartans:latest'
      }
    }
   
   stage("App deployment started"){
     sh 'oc login --token=VQUyTz1TcNmkHU8d9of0D4HZdkC6nXLozsuZg7njj9g --server=https://api.us-west-1.starter.openshift-online.com:6443'
     sh 'oc project itrainspartans'
     //sh 'oc new-app --name py-mani manee2k6/py-spartans'
      sh 'oc rollout latest dc/py-mani -o json' 
      sh 'oc rollout latest madhu/py-newrelic --name python \
          --env NEWRELIC_LICENSE=xxxxxx \
                NEWRELIC_APPNAME=pyapp'
     //sh 'oc expose svc py-mani' 
    }
   
    stage('App deployed to Openshift environment') {
     echo 'App deployed to Openshift environment..'
    }

  }
