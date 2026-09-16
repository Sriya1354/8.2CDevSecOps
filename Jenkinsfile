pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Sriya1354/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
            post {
                always {
                    emailext(
                        subject: "Test Stage - ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                        body: """<p>Test stage completed with status: <b>${currentBuild.currentResult}</b></p>
                                 <p>Job: ${env.JOB_NAME}</p>
                                 <p>Build Number: ${env.BUILD_NUMBER}</p>
                                 <p>Check console output at: ${env.BUILD_URL}</p>""",
                        to: 'your_email@example.com',
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
            post {
                always {
                    emailext(
                        subject: "Security Scan Stage - ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                        body: """<p>Security scan (npm audit) completed with status: <b>${currentBuild.currentResult}</b></p>
                                 <p>Job: ${env.JOB_NAME}</p>
                                 <p>Build Number: ${env.BUILD_NUMBER}</p>
                                 <p>Check console output at: ${env.BUILD_URL}</p>""",
                        to: 'your_email@example.com',
                        attachLog: true
                    )
                }
            }
        }
    }
}