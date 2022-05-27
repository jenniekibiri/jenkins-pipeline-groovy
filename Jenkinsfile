#!/usr/bin/env groovy
//import groovy script
def gv

pipeline {
    agent any
    environment {
        SERVER_CREDENTIALS =  credentials('githubcredentials')
    }
    parameters {
        choice(name:'VERSION', choices:['1.0', '1.1', '1.2'], description:'Choose the version of the project')

        booleanParam(name :'executeTests', description:'Execute the tests', defaultValue:false)
    }
    stages {
        stage('init') {
            steps {
                script {
                    gv = load('./script.groovy')
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    gv.buildApp()
                }
            }
        }
        stage('Test') {
            when {
                expression {
                    params.executeTests
                }
            }

            steps {
                script {
                    gv.testApp()
                }
            }
        }

        stage('Deploy') {
            input {
                message 'select the environment to deploy to'
                ok 'Deploy'
                parameters {
                    choice(name :'one', choices:['dev', 'test', 'prod'], description:'Choose the environment to deploy to')
                    choice(name :'two', choices:['dev', 'test', 'prod'], description:'Choose the environment to deploy to')
                }
            }
            steps {
                //credentials
                withCredentials([
                usernamePassword(credentials:'githubcredentials', usernameVariable:'USER', passwordVariable:'PASSWORD')
                ]) {
                    echo  "some script ${USER}"
                }
                script {
                    gv.deployApp()
                    echo "deploying with credentials: ${SERVER_CREDENTIALS}"
                }
            }
        }
    }
}
