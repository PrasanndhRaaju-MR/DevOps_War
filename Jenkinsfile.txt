pipeline {
    agent any

    stages {
        stage('scm') {
            steps {
        git branch: 'main', url: 'https://github.com/PrasanndhRaaju-MR/DevOps_War.git'
            }
        }
        stage('build') {
            steps {
               sh "mvn clean"
               sh "mvn install"
}
}
stage('build to images') {
            steps {
               script{
                  sh 'docker build -t prasnndh/simplewebapp .'
               }
    }
}
stage('push to hub') {
            steps {
               script{
                 withDockerRegistry(credentialsId: 'Demo', url: 'https://index.docker.io/v1/') {
                  sh 'docker push prasnndh/simplewebapp'
               }
            }
            }
}
}
}