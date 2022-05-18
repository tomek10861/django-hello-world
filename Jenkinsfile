pipeline {
    agent { node { label 'dev' } }

    environment {
    POSTGRES_HOST = credentials('POSTGRES_HOST')
    POSTGRES_DB = credentials('POSTGRES_DB_DEV')
    POSTGRES_USER = credentials('POSTGRES_USER_DEV')
    POSTGRES_PASSWORD = credentials('POSTGRES_PASSWORD_DEV')
    }

    def scmVars

    stages {
        stage('Git clone') {
            scmVars = git branch: 'dev', changelog: false, credentialsId: '1a83e8db-8990-44e5-8402-d991ecc3b7f1', poll: true, url: 'https://github.com/tomek10861/django-hello-world.git'

            echo "GIT_BRANCH is ${scmVars.GIT_BRANCH}"
            echo "GIT_COMMIT is ${scmVars.GIT_COMMIT}"
            echo "GIT_AUTHOR_NAME is ${scmVars.GIT_AUTHOR_NAME}"
        }
    }
}
