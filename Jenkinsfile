#!/usr/bin/env groovy

def gv

pipeline {
    agent any
    parameters{
        
    choice( name :'version', choices:['1.0','1.1','1.2'],description:'Choose the version of the project' )
    booleanParam( name :'executeTests', description:'Execute the tests', defaultValue:false )
    }
    stages {
        stage("init"){
            steps{
                script{
                     gv = load "script.groovy"
                } 
            }
        }
        stage('Build') {
            steps {
                script{
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
            script{
                gv.testApp()
            }
                }
        }
      
        
        stage('Deploy') {
            steps {script{
                    gv.deployApp()
                }
            }
            
        }
    }
}
