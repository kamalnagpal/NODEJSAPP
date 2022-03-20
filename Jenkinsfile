pipeline {
    agent any

//    options {
//      timeout(time: 5, unit: 'MINUTES') 
//    }
    stages {
        stage('Git Clone') {
            steps {
               git branch: 'main', url: 'https://github.com/kamalnagpal/NODEJSAPP.git'
            }
        }
        
        stage('build docker image') {
            steps {
                sh 'sudo docker build . -t nodejs'
                sh 'sudo docker run -d -p 8083:3000 nodejs'
                sh 'sudo docker image tag nodejs:latest dockeridavailable/nodejs:latest'
                sh 'sudo docker push dockeridavailable/nodejs:latest'
                sh 'kubectl apply -f ./node-js-kubernetes-deployment.yml'
                sh 'kubectl autoscale deployment node-js --cpu-percent=50 --min=1 --max=10'
            }
        }
    }
}
