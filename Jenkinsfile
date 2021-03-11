pipeline {
    agent { label 'master' }
    stages {
        stage('DEV') {
            environment {
                BUILD_REQUESTEDFOREMAIL = sh (script: 'git --no-pager show -s --format=\'%ae\'', returnStdout: true).trim()
                BUILD_REQUESTEDFOR = sh (script: 'git --no-pager show -s --format=\'%an\'', returnStdout: true).trim()
            }
            steps {
              sh '''#!/bin/bash
                    MSG=$(git log -1 --format=%B)
                    rsync -avr --exclude='.git' --exclude='.github' https://github.com/KuzRomanDocker/Task3
                    cd target-repo
                    git checkout release-candidate
                    git config user.email ${BUILD_REQUESTEDFOREMAIL}
                    git config user.name ${BUILD_REQUESTEDFOR}
                    git add .
                    git commit -m "${MSG}"
                    git push"
                   '''
            }
        }
    }
