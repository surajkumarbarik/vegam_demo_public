pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/demo_public']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_cred', url: 'https://github.com/surajkumarbarik/vegam_demo_public.git']])
            }
        }
        stage('SonarQube analysis') {
            def scannerHome = tool 'sonarqube';
            withSonarQubeEnv(credentialsId: 'sonar_token') {
                sh "${scannerHome}/bin/sonar-scanner \
                -D sonar.login=admin \
                -D sonar.password=sonarcube \
                -D sonar.projectKey=vegam_demo_public \
                // -D sonar.exclusions=vendor/**,resources/**,**/*.java \
                -D sonar.host.url=http://192.168.152.42:9099/"
            }
        }
        
        
    }
}



