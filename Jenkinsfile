    def gitClone(nodeEnv) {
        git branch: nodeEnv, changelog: false, credentialsId: '1a83e8db-8990-44e5-8402-d991ecc3b7f1', poll: true, url: 'https://github.com/tomek10861/django-hello-world.git'

        branch = sh (
            script: 'git --no-pager show -s --format=\'%d\' | cut -d\'>\' -f2 | cut -d\',\' -f1',
            returnStdout: true
        ).trim()
        commit = sh (
            script: 'git --no-pager show -s --format=\'%h\'',
            returnStdout: true
        ).trim()
        msg = sh (
            script: 'git --no-pager show -s --format=\'%s\'',
            returnStdout: true
        ).trim()
        author = sh (
            script: 'git --no-pager show -s --format=\'%cn\'',
            returnStdout: true
        ).trim()

    sh """#!/bin/bash
    echo \"#git repository\" > buildinfo.txt
    echo \"branch=${branch}\" >> buildinfo.txt
    echo \"commit=${commit}\" >> buildinfo.txt
    echo \"msg=${msg}\" >> buildinfo.txt
    echo \"author=${author}\" >> buildinfo.txt
    """

          }

pipeline {
        agent { node { label params.NODE } }

          environment {
          POSTGRES_HOST = credentials('POSTGRES_HOST')
          POSTGRES_DB = credentials('POSTGRES_DB_DEV')
          POSTGRES_USER = credentials('POSTGRES_USER_DEV')
          POSTGRES_PASSWORD = credentials('POSTGRES_PASSWORD_DEV')
          }

          stages {
          stage('Git clone dev') {
              when { expression {  params.NODE == 'dev' } }
              steps {
                  gitClone('dev')
              }
          }

          stage('Git clone prod') {
              when { expression {  params.NODE == 'prod' } }
              steps {
                  gitClone('main')
              }
          }
          stage('Build env file') {
            steps {
                  sh '''#!/bin/bash
                  echo "DEBUGAPP=FALSE" > .env
                  echo "POSTGRES_NAME=$POSTGRES_DB" >> .env
                  echo "POSTGRES_USER=$POSTGRES_USER" >> .env
                  echo "POSTGRES_PASSWORD=$POSTGRES_PASSWORD" >> .env
                  echo "POSTGRES_HOSTDBNAME=$POSTGRES_HOST" >> .env
                  echo "POSTGRES_PORT=5432" >> .env
                  cat buildinfo.txt
                     '''
            }
          }

          stage('Build and run docker') {
            steps {
                  sh "docker-compose --profile dev_prod build"
                  sh "docker-compose --profile dev_prod up -d"
            }
          }

        stage('CleanWorkspaceAfter') {
             steps {
                 cleanWs()
             }
         }
        }
  }
