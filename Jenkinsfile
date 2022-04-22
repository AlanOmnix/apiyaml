node {

    stage('Clone repository') {

        checkout scm

    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                    sh "git config user.email asolano@omnixcorp.com"
                    sh "git config user.name AlanOmnix"
                    //sh "git switch master"
                    sh "cat deployApi.yaml"
                    sh "sed -i 's+alanx30/ecommercemodulo_apinode.*+alanx30/ecommercemodulo_apinode:${DOCKERTAG}+g' deployApi.yaml"
                    sh "cat deployApi.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/apiyaml.git HEAD:master"
                }
            }
        }
    }   
}