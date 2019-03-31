pipeline {
    agent {
        docker {image 'maven:3.3.3'}
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
                sh ```
                    echo "multiline shell steps" 
                    ls -lah
                    ```
            }
        }
    }
}