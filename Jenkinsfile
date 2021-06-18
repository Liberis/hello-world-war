pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'mvn install'
                    }
                }
        stage('check'){
            steps{
                
                step([$class: 'HelloWorldBuilder', name:'Liberis'])
               } 
            }
        }
    }
