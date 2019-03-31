pipeline {
    agent {
        docker {image 'maven:3.3.3'}
    }
    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE = 'sqlite'
        AWS_ACCESS_KEY_ID = credentials('jenkins-aws-secret-key-id')
        AWS_ACCESS_KEY_SECRET = credentials('jenkins-aws-secret-access-key')
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
                sh 'printenv'
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

        stage('deploy -- staging') {
            steps {
                sh 'echo "Running the smoking tests"'
            }
        }

        stage('Sanity check') {
            steps {
                // input "Does the staging environment look ok?"
                echo "Is everything ok?"
            }
        }

        stage('deploy -- production') {
            steps {
                sh 'echo "Deploying"'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
            // slackSend channel: '#my-project',
            //       color: 'good',
            //       baseUrl: 'yukuansong.slack.com',
            //       tokenCredentialId: 'xoxp-573413843862-573049175751-571402292289-6a9ac893b0040a42ceea9e27916f442c',
            //       message: "The pipeline ${currentBuild.fullDisplayName} completed successfully."
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