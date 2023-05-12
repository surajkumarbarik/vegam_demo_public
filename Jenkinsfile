// this is the public repo's jenkins file




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

        stage('Install Dependencies') {
            steps {
                bat 'C:/Users/suraj/AppData/Local/Programs/Python/Python310/Scripts/pip.exe install -r requirements.txt'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'C:/Users/suraj/AppData/Local/Programs/Python/Python310/Scripts/pytest.exe'
            }
        }

        // stage('SonarQube Scan') {
        //     // environment {
        //     //     scannerHome = tool 'sonarqube'
        //     // }
        //     // steps {
        //     //     bat 'sonar-scanner -Dsonar.projectKey=vegam_demo_public -Dsonar.sources=. -Dsonar.host.url=http://192.168.152.42:9099 -Dsonar.login=admin -D sonar.password=sonarcube'
        //     // }


        //     steps {
        //         withSonarQubeEnv('SonarQube') {
        //             bat 'C:\\ProgramData\\Jenkins\\.jenkins\\tools\\hudson.plugins.sonar.SonarRunnerInstallation\\sonarqube\\bin";%PATH% && sonar-scanner.bat'
        //         }
        //     }
        // }




        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    bat "${tool ('sonarqube')}/bin/sonar-scanner \
                    -D sonar.login=admin \
                    -D sonar.password=sonarcube \
                    -D sonar.projectKey=check_git_action \
                    -D sonar.host.url=http://192.168.0.112:9099/"
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                    println "completed"
                    echo "completed"
                }
            }
        }

    }
    post {
        always {
            script {
                try {
                    // Your pipeline code goes here
                    currentBuild.currentResult = 'SUCCESS'
                    embeddableBuildBadge()
                } catch (Exception e) {
                    currentBuild.currentResult = 'FAILURE'
                    embeddableBuildBadge()
                }
            }
        }
    }
//     post {
//         always {
//             // Update the pull request status on GitHub
//             githubPullRequest status: 'SUCCESS',
//             message: 'The build passed!',
//             accessTokenCredentialId: 'github-api-token',
//             context: 'Jenkins Build'
//         }
//   }




 





        // stage("SonarQube Gatekeeper") {
        //     steps {
        //         script {
        //             withSonarQubeEnv('SonarQube') {
        //                 bat 'set PATH="C:\\ProgramData\\Jenkins\\.jenkins\\tools\\hudson.plugins.sonar.SonarRunnerInstallation\\sonarqube\\bin";%PATH% && sonar-scanner.bat'
        //                 def qualitygate = waitForQualityGate()
        //                 echo qualitygate
        //                 if (qualitygate.status != "OK") {
        //                     error "Pipeline aborted due to quality gate coverage failure: ${qualitygate.status}"
        //                 } 
        //                 else {
        //                     echo "Pipeline succeded due to quality gate coverage successfull: ${qualitygate.status}"
        //                 }
        //             }
        //         }
        //     }
        // }
    
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



