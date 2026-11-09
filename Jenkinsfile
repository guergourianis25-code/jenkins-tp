def gv

pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    parameters {
        string(name: 'VERSION', defaultValue: '1.0.0', description: 'version à déployer')
        choice(name: 'VERSION_CHOIX', choices: ['1.1.0', '1.2.0', '1.3.0'], description: 'choisir la version')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'lancer les tests ?')
    }

    environment {
        NEW_VERSION = '1.3.0'
    }

    stages {
        stage('init') {
            steps {
                script { gv = load "script.groovy" }
            }
        }
        stage('build') {
            steps {
                echo "building version ${NEW_VERSION}"
                bat 'mvn --version'
                script { gv.buildApp() }
            }
        }
        stage('test') {
            when {
                expression { params.executeTests }
            }
            steps {
                script { gv.testApp() }
            }
        }
        stage('deploy') {
            steps {
                script { gv.deployApp() }
            }
        }
    }

    post {
        always  { echo 'pipeline terminé' }
        success { echo 'build réussi' }
        failure { echo 'build échoué' }
    }
}
