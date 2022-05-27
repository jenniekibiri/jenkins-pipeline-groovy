pipeline {
    agent any
    parameters{
        
     choice( name :'version', choices:['1.0','1.1','1.2'],description:'Choose the version of the project' )
    booleanParam( name :'executeTests', description:'Execute the tests', defaultValue:false )
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
            
        }
    }
}
