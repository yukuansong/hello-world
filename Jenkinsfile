pipeline {
    agent {
        docker {image 'maven:3.3.3'}
    }
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE = 'sqlite'
        AWS_ACCESS_KEY_ID = credentials('jenkin-aws-access-key-id')
        AWS_ACCESS_KEY_SECRET = credentials('jenkin-aws-access-key-secret')
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('test') {
            steps {
                sh 'printenv'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
            mail to: 'yukuan.song@gmail.com',
                 subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                 Body: "The build is successful!"
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}