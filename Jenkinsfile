#!/usr/bin/env groovy

pipeline {
    agent none
    triggers {
        cron('*/10 * * * *')
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        timeout(time: 1, unit: 'HOURS')
        timestamps()
    }

    stages {
        stage('Build Stage') {
            agent none
            // agent { docker 'centos' }
            steps {
                parallel(
                    'create-folders' : {
                        sh 'mkdir -p dist/bin'
                        sh 'mkdir -p bin'
                    },
                    'touch-files' : {
                        sh 'touch 1.txt'
                        sh 'touch 2.txt'
                        sh 'touch 3.txt'
                    },
                )
            }
        }

        stage('Test Stage') {
            agent none
            environment {
                GIT_COMMITTER_EMAIL = 'demo@doit.com'
                GIT_COMMITTER_NAME = 'Do'
                GIT_AUTHOR_NAME = 'The'
                GIT_AUTHOR_EMAIL = 'demo@doit.com'
            }

            steps {
                sh 'env && echo "oy! did test"'
            }
        }
    }
}
// vim: ft=groovy
