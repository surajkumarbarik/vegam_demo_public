// pipeline {
//     agent any
    
//     stages {
//         stage('Checkout') {
//             steps {
//                 checkout scmGit(branches: [[name: '*/demo_public']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_cred', url: 'https://github.com/surajkumarbarik/vegam_demo_public.git']])
//             }
//         }
//             stage('Clone the Git') {
//                 git branch: 'demo_public', credentialsId: 'git_cred_1', url: 'https://github.com/surajkumarbarik/vegam_demo_public.git'
//             }
            
//     }
// }



pipeline {
    agent any
    
    stages {
        stage('checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/demo_public']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_cred', url: 'https://github.com/surajkumarbarik/vegam_demo_public.git']])
            }
        }
        
        stage('clone') {
            steps {
                git branch: 'demo_public', credentialsId: 'git_cred_1', url: 'https://github.com/surajkumarbarik/vegam_demo_public.git'
            }
        }

        stage('SonarQube Scan') {
            environment {
                scannerHome = tool 'sonarqube'
            }
            // steps {
            //     bat 'sonar-scanner -Dsonar.projectKey=vegam_demo_public -Dsonar.sources=. -Dsonar.host.url=http://192.168.152.42:9099 -Dsonar.login=admin -D sonar.password=sonarcube'
            // }


            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'set PATH="C:\\Sonar Qube Work Drive\\sonar-scanner-4.7.0.2747-windows\\bin";%PATH% && sonar-scanner.bat'
                }
            }
        }




        // stage('SonarQube Scan') {
        //     steps {
        //         withSonarQubeEnv('sonarqube') {
        //             bat "sonarqube/bin/sonar-scanner \
        //             -D sonar.login=admin \
        //             -D sonar.password=sonarcube \
        //             -D sonar.projectKey=vegam_demo_public \
        //             -D sonar.host.url=http://192.168.152.42:9099/"
        //         }
        //     }
        // }
    }
}







  
        // stage('SonarQube analysis') {
        //     def scannerHome = tool 'sonarqube';
        //     withSonarQubeEnv(credentialsId: 'sonar_token') {
        //         sh "${scannerHome}/bin/sonar-scanner \
        //         -D sonar.login=admin \
        //         -D sonar.password=sonarcube \
        //         -D sonar.projectKey=vegam_demo_public \
        //         // -D sonar.exclusions=vendor/**,resources/**,**/*.java \
        //         -D sonar.host.url=http://192.168.152.42:9099/"
        //     }
        // }
        
        
//     }
// }



