pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                echo 'building the application...'
            }
        }
        stage('test') {
            when {
                expression { env.BRANCH_NAME == 'dev' || env.BRANCH_NAME == 'main' }
            }
            steps {
                echo 'testing the application...'
            }
        }
        stage('deploy') {
            steps {
                echo 'deploying the application...'
            }
        }
    }

    post {
        always  { echo 'pipeline terminé' }
        success { echo 'build réussi' }
        failure { echo 'build échoué' }
    }
}
