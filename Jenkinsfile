pipeline {
    agent any

    stage('Clone repository') {
         steps {
                // Clone the repository that contains your Node.js app and Dockerfile
                git branch: 'main',changelog: false, poll: false, url: 'https://github.com/seynath/Ecommerce-all-CICD.git'
            }
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email thenura-im20102@stu.kln.ac.lk"
                        sh "git config user.name seynath"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+seynath/ecomserver.*+seynath/ecomserver:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Ecommerce-all-CICD.git HEAD:main"
      }
    }
  }
}
}
