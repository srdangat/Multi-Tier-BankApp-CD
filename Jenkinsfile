pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'git@github.com:srdangat/Multi-Tier-BankApp-CD.git'
            }
        }
        stage('K8s Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'project-cluster', contextName: '', credentialsId: 'k8s-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://3621726323D8AC4C06C32B358630B714.gr7.us-east-1.eks.amazonaws.com') {
                    sh "kubectl apply -f database/database-ds.yml"  // Corrected folder name
                    sh "kubectl apply -f bankapp/bankapp-ds.yml"
                    sleep 30
                    sh "kubectl get pods -n webapps"
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
