pipeline {
    agent any
    triggers{ pollSCM('*/1 * * * *') }

    stages {
        stage('Buvejuma-izveide') {
            steps {
                script{
                    build()
                }
        }
        }

        stage('Bvejuma-izvietosana-dev-vide') {
            steps {
                script{
                    deploy("DEV", 1010)
                }
            }
        }

        stage('Testu-izpilde-dev-vide') {
            steps {
                script{
                    test("DEV")
                }
            }
        }

        stage('Bvejuma-izvietosana-stg-vide') {
            steps {
                script{
                    deploy("STG", 2020)
                }
            }
        }

        stage('Testu-izpilde-stg-vide') {
            steps {
                script{
                    test("STG")
                }
            }
        }

        stage('Bvejuma-izvietosana-prd-vide') {
            steps {
                script{
                    deploy("PRD", 3030)
                }
            }
        }

        stage('Testu-izpilde-prd-vide') {
            steps {
               script{
                    test("PRD")
                }
            }
        }
    }
}

def build(){
    echo "Building to enviroment started.."
    //for windows: bat "npm.."
    bat "dir"
    bat "npm install"
}


def deploy(String enviroment, int port){
    echo "Deployment to ${environment} has started.."
    bat "npm install"
    bat "dir"
    bat "node_modules\\.bin\\pm2 delete \"books-${environment}\" || exit 0"
    bat "node_modules\\.bin\\pm2 start -n \"books-${environment}\" index.js -- ${port}"
}

def test(String enviroment){
    echo "Testing to ${enviroment} started.."
}

