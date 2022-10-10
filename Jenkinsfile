// pipeline {
//     environment {
//         // overwriting default cache directory
//         NPM_CONFIG_CACHE = "${WORKSPACE}/.npm"
//     }
//     agent {
//         docker {
//             image 'node:6-alpine'
//             args '-p 3000:3000'
//         }
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 echo 'Building..'
//                 sh 'npm i'
//             }
//         }
//         stage('Test') {
//             steps {
//                 echo 'Testing..'
//                 sh 'npm test'
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 echo 'Deploying..'
//                 echo 'Deployed!'
//             }
//         }
//     }
// }


// Using docker compose

pipeline {
    agent any
    
    stages {
        stage("verify tooling") {
            steps {
                sh '''
                    docker info
                    docker version
                    docker-compose -v
                    curl --version
                    docker ps
                '''
            }
        }
        stage("Prune docker data") {
            steps {
                sh 'docker system prune -a --volumes -f'
            }
        }
        stage('Starting containers') {
            steps {
                sh 'docker compose up -d --wait'
                sh 'docker compose ps'
            }
        }
    }
}