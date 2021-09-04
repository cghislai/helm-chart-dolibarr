pipeline {
    agent {
        label 'cluster-manager'
    }
    parameters {
        booleanParam(name: 'FORCE_PUSH', defaultValue: false, description: 'Force push')
        string(name: 'REPO', defaultValue: 'https://nexus.valuya.com/service/rest/v1/components?repository=helm', description: 'Alternative deployment repo')
        credentials(name: 'REPO_CREDENTIAL',description: 'Repo credentials',credentialType: "Username with password", required: false,
         defaultValue: 'jenkins-jenkins-nexus-credentials')
  }
    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }
    stages {
        stage ('Push') {
            when { anyOf {
              environment name: 'BRANCH_NAME', value: 'master'
              expression { return params.FORCE_PUSH == true }
            } }
            steps {
                container('manager') {
                    withCredentials([usernamePassword(credentialsId: params.REPO_CREDENTIAL, passwordVariable: 'PASSWORD', usernameVariable: 'USER')]) {
                        sh "helm dependency update"
                        sh '''
                            OUT="$(helm package ".")"
                            OUT_PATH="$(echo "$OUT" | cut -d':' -f2)"
                            echo "Packaged $CHART_PATH to $OUT_PATH"

                            curl --fail -vF file=@"$OUT_PATH" -u"${USER}:${PASSWORD}" "${REPO}" \
                             && echo "Pushed to $REPO" || (echo "!!! FAILED TO PUSH ($?)" && exit 1)
                        '''
                    }
                }
            }
             post {
                failure {
                  echo "Push failed"
                }
             }
        }
    }
    post {
        failure {
          mail(
            to: 'charlyghislain@gmail.com', cc: 'yannick@valuya.be',
            subject: "Build failed: helm-charts/dolibarr $BRANCH_NAME ${BUILD_NUMBER}",
            body: "See job at ${BUILD_URL}"
          )
        }
    }
}
