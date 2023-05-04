pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/demo_public']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_cred', url: 'https://github.com/surajkumarbarik/vegam_demo_public.git']])
            }
        }
        stage('SonarQube Analysis') {
            def scannerHome = tool 'SonarScanner';
            withSonarQubeEnv(credentialsId: 'sonar_token') {
                sh "${scannerHome}/bin/sonar-scanner"
            }
        }
        
        
    }
}




