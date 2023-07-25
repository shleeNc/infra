
  node {

      stage('Clone repository') {
          checkout scm
      }

      stage('Fargate Task call') {
          withCredentials([usernamePassword(credentialsId: 'twistlockDefenderManager', passwordVariable: 'TL_PASS', usernameVariable: 'TL_USER')]) {
              sh 'curl -s -k -u $TL_USER:$TL_PASS https://api.sg.prismacloud.io/api/v1/defenders/fargate.json?consoleaddr=api.sg.prismacloud.io -X POST -H "Content-Type:application/json" --data-binary "@fargate.json" | jq . > tw_fargate.json'
              sh 'cat tw_fargate.json'
          }
      }

      stage('Publish Function') {
          archiveArtifacts artifacts: 'tw_fargate.json'}
  }

