pipeline {
    agent none

    stages {
        
        stage('clean up') {
        	steps {
                cleanWs()
            }
        } //End stage
        
        stage('clear existing dontainer') {
        	steps {
                sh'''
                  docker-compose stop
                '''
            }
        } //End stage
        
        stage('deploy docker container') {
        	steps {
                sh'''
                  docker-compose up -d
                '''
            }
        } //End stage
    }//End stages
}//End pipeline
