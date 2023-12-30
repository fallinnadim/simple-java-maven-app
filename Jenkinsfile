// node {
//     docker.image('maven:3.9.5-eclipse-temurin-17-alpine').inside('-v /root/.m2:/root/.m2') {
//         stage('Build') {
//             sh 'mvn -B -DskipTests clean package'
//         }
//         stage('Test') {
//             try {
//                 sh 'mvn test'
//             } catch (e){
//                 echo 'test went wrong'
//                 throw (e)
//             } finally {
//                 junit 'target/surefire-reports/*.xml'
//             }
//         }
//         stage('Manual Approval') {
//             input message: 'Lanjut ke tahap Deploy? (Klik "Proceed" untuk mengakhiri)'
//         }
//         stage('Deploy') {
//             sh './jenkins/scripts/deliver.sh'
//         }
//     }
// }

pipeline {
    agent {
        docker {
            image 'maven:3.9.5-eclipse-temurin-17-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjut ke tahap Deploy? (Klik "Proceed" untuk mengakhiri)' 
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}