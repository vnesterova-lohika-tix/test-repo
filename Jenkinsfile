node('master') {
    parameters {
        choice(choices:['Freeze', 'Unfreeze'], description: 'Freeze or unfreeze branch from merging', name: 'ACTION')
        choice(choices:['master', 'hotfix*'], description: 'Choose branch', name: 'BRANCH')
        //choice(choices:['5','4'], description: 'Choose PR if you want to unfreeze it', name: 'PR')
        gitParameter name: 'PR', type: 'PT_PULL_REQUEST', defaultValue: '5', sortMode: 'DESCENDING_SMART'
        gitParameter name: 'BRANCH', type: 'PT_BRANCH', defaultValue: 'master', sortMode: 'DESCENDING_SMART'
    }

        // stage('Manual Step') {

        //         echo "choice: ${ACTION}"
        //         echo "choice params.: " + params.BRANCH
        //         echo "choice env: " + env.PR

        // }

            if (env.ACTION == 'Freeze') {
        stage('Freezing') {
                sh """
 curl -d "frozen=true&user_name=Scooby Doo" -X POST 'https://www.mergefreeze.com/api/branches/vnesterova-lohika-tix/test-repo/master/?access_token=658a3396-ffad-41c2-8db5-07d023d047d0'
 """
            echo 'You have frozen the branch'
        }

            }

               else {
        stage('Unfreezing') {
            if (env.ACTION == 'Unfreeze') {
                sh """
 curl -d "frozen=false&user_name=Scooby Doo" -X POST 'https://www.mergefreeze.com/api/branches/vnesterova-lohika-tix/test-repo/master/?access_token=658a3396-ffad-41c2-8db5-07d023d047d0'
 """
                echo 'You have unfrozen the branch'
            }
        }
               }
    stage('Unfreeze specific PR') {
        if ('${params.PULL_REQUESTS}' == 'master') {
            sh """
                     curl -d "frozen=false&unblocked_prs=[5]" -X POST 'https://www.mergefreeze.com/api/branches/vnesterova-lohika-tix/test-repo/master/?access_token=658a3396-ffad-41c2-8db5-07d023d047d0'
                     """
        }
                 else {
            echo 'skip'
                 }
    }
}
