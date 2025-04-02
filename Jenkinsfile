pipeline {
    agent any
    triggers{ pollSCM('*/1 * * * *') }

    stages {
        stage('Build') {
            steps {
                script{
                    build()
                }
        }
        }

        stage('Deploy to DEV') {
            steps {
                script{
                    deploy("DEV", 1010)
                }
            }
        }

        stage('Tests on DEV') {
            steps {
                script{
                    test("BOOKS", "DEV")
                }
            }
        }

        stage('Deploy to STG') {
            steps {
                script{
                    deploy("STG", 2020)
                }
            }
        }

        stage('Tests on STG') {
            steps {
                script{
                    test("BOOKS", "STG")
                }
            }
        }

        stage('Deploy to PRD') {
            steps {
                script{
                    deploy("PRD", 3030)
                }
            }
        }

        stage('Tests on PRD') {
            steps {
               script{
                    test("BOOKS","PRD")
                }
            }
        }
    }
}

def build(){
    echo "Building of node application has started..."
    //for windows: bat "npm.."
    bat "dir"
    bat "npm install"
    //bat "npm test"
}


def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    //git branch: 'jenkins_pipeline_windows', poll: false, url: 'https://github.com/n1ckyg/sample-book-app.git'
    //bat "npm install"
    //bat "dir"
    bat "node_modules\\.bin\\pm2 delete \"books-${environment}\" || exit 0"
    bat "node_modules\\.bin\\pm2 start -n \"books-${environment}\" index.js -- ${port}"
    // bat "pm2 list"
    //bat "pm2 delete \"books-${environment}\" || exit 0"
    //bat "pm2 start -n \"books-${environment}\" index.js -- ${port}"
    //bat "pm2 list"
}

def test(String test_Set, String environment){
    echo "Testing ${test_Set} test set to ${environment} started.."
    git branch: '', poll: false, url: 'https://github.com/n1ckyg/api-automation.git'
    bat "npm install"
    bat "npm run ${test_Set} ${test_Set}_${environment}"
}

