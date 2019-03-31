pipeline {
    agent {
        docker {image 'maven:3.3.3'}
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
                sh '''
                    echo "multiline shell steps" 
                    ls -lah
                    '''
                    sh 'mvn clean install'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}