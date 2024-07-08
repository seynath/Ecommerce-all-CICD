pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                // Clone the repository that contains your Node.js app and Dockerfile
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/seynath/Ecommerce-all-CICD.git'
            }
        }

        stage('Update GIT') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            // Setting up Git configuration
                            sh "git config user.email 'thenura-im20102@stu.kln.ac.lk'"
                            sh "git config user.name 'seynath'"
                            // Display current content of deployment.yaml
                            sh "cat deployment.yaml"
                            // Replace the docker image tag with the new tag in deployment.yaml
                            sh "sed -i 's+seynath/ecomserver.*+seynath/ecomserver:${env.BUILD_NUMBER}+g' deployment.yaml"
                            // Display updated content of deployment.yaml
                            sh "cat deployment.yaml"
                            // Add changes to git
                            sh "git add ."
                            // Commit changes
                            sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                            // Push changes
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Ecommerce-all-CICD.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}
