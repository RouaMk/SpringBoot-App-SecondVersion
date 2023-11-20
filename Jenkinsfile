pipeline {
    agent any

    stages {
        stage("Getting Code") {
            steps {
                git url: 'https://github.com/RouaMk/SpringBoot-App-SecondVersion.git', branch: 'main',
                credentialsId: 'github-credentials' // jenkins-github-creds
                sh "ls -ltr"
            }
        }

        stage("Build and Package") {
            steps {
                script {
                    echo "======== Executing Build and Package ========"
                    sh "mvn clean package"
                }
            }
        }

        stage("Unit Tests") {
            steps {
                script {
                    echo "======== Executing Unit Tests ========"
                    sh "mvn test"
                }
            }
        }

        stage("Code Quality Analysis with SonarQube") {
            steps {
                script {
                    echo "======== Executing SonarQube Analysis ========"
                    withSonarQubeEnv('SonarQubeServer') {
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }

        stage("Create Docker Image") {
            steps {
                script {
                    echo "======== Executing Docker Image Creation ========"
                    sh "docker build -t devopstp ."
                }
            }
        }

        stage("Push to Docker Hub") {
            steps {
                script {
                    echo "======== Executing Push to Docker Hub ========"
                    sh "docker tag devopstp rouamk/devopstp:devopstp"
                    sh "docker push rouamk/devopstp:devopstp"
                }
            }
        }
    }

    post {
        success {
            echo "======== Pipeline executed successfully ========"
        }
        failure {
            echo "======== Pipeline execution failed ========"
        }
    }
}
