node('master') {
  //may be skipped
  BUILD_TRIGGER_BY = "${currentBuild.getBuildCauses()[0].userName}"

  parameters {
    string(name: 'BRANCH', defaultValue: 'master', description: 'Choose branch')
    choice(choices: ['Freeze', 'Unfreeze'], description: 'Freeze or unfreeze branch from merging', name: 'ACTION')
  }

  withCredentials([string(credentialsId: 'ORG_TOKEN', variable: 'ORG_TOKEN')]) {
    //add here repos for umbrella
    def repos = ['repo1', 'repo2']
    repos.each() {



      switch (params.ACTION) {
      case "Freeze":
        bool = true
        stage('Freezing') {

          sh """
          curl -d "account=vnesterova-test-organization&repository=${it}&branch=$params.BRANCH&frozen=$bool&user_name=${BUILD_TRIGGER_BY}&access_token=$ORG_TOKEN" -X POST 'https://www.mergefreeze.com/api/branches'
          """ 
        }
        break
      case "Unfreeze":
        bool = false
        stage('Unfreezing') {

          sh """
           curl -d "frozen=false&user_name=Valeriia Nesterova" -X POST 'https://www.mergefreeze.com/api/branches/vnesterova-test-organization/${it}/$params.BRANCH/?access_token=$ORG_TOKEN'
          """

        }
        break
      default:
        result = "no such branch"
        break
      }

    }
  }
}
