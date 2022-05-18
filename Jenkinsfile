pipeline {
    agent { node { label 'dev' } }

    environment {
    POSTGRES_HOST = credentials('POSTGRES_HOST')
    POSTGRES_DB = credentials('POSTGRES_DB_DEV')
    POSTGRES_USER = credentials('POSTGRES_USER_DEV')
    POSTGRES_PASSWORD = credentials('POSTGRES_PASSWORD_DEV')
    }


    stages {
        stage('Git clone') {
            steps {
            echo "Hello World"
            git branch: 'dev', changelog: false, credentialsId: '1a83e8db-8990-44e5-8402-d991ecc3b7f1', poll: false, url: 'https://github.com/tomek10861/django-hello-world.git'
            echo GIT_COMMIT %GIT_COMMIT%
            echo GIT_BRANCH %GIT_BRANCH% 
            echo GIT_LOCAL_BRANCH %GIT_LOCAL_BRANCH%
            echo GIT_PREVIOUS_COMMIT %GIT_PREVIOUS_COMMIT%
            echo GIT_PREVIOUS_SUCCESSFUL_COMMIT %GIT_PREVIOUS_SUCCESSFUL_COMMIT%
            echo GIT_URL %GIT_URL%
            echo GIT_URL_N - %GIT_URL_N%
            echo GIT_AUTHOR_NAME %GIT_AUTHOR_NAME%
            echo GIT_COMMITTER_EMAIL %GIT_COMMITTER_EMAIL%
            }
        }
    }
}
