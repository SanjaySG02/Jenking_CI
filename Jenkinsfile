pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Java Application'
                sh 'pwd'
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying JAR file'
                sh '''
                    mkdir -p /opt/array-sum-deployment
                    cp target/sum_of_numbers.jar /opt/array-sum-deployment/
                '''
            }
        }

        stage('Execute') {
            steps {
                echo 'Executing deployed application'
                sh '''
                    cd /opt/array-sum-deployment
                    printf "10\\n20\\n30\\n40\\n50\\n" | java -jar sum_of_numbers.jar
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}