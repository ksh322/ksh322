pipeline {
  agent any
  stages {
    stage(' git clone or git pull' ) {
      steps {
        git url: 'https://github.com/beomtaek/test2.git', branch: 'master'
      }
    }

    stage(' docker image build and push to p-registry' ) {
      steps {
        sh '''
        docker build -t 192.168.8.100:5000/testweb:blue .
        docker push 192.168.8.100:5000/testweb:blue
        '''
      }
    }

    stage(' deployment, svc creation ' ) {
      steps {
        sh '''
        kubectl create deploy testweb3 --image=192.168.8.100:5000/testweb:blue
        kubectl expose deploy testweb3 --type=LoadBalancer --port=80 --target-port=80 --name=testweb3-svc
        '''
      }
    }
  }
}
