pipeline {
    agent any
    stages {
        stage('Lint HTML'){
            steps{
                sh 'tidy -q -e *.html'
            }
        }
        stage('Upload to AWS'){
            steps{
                withAWS(credentials:'aws-static') {
                    s3Upload(file:'index.html', bucket:'jenkins-udacity-mustafa', path:'index.html')
                }
            }
        }
        stage('Validate deployment'){
            steps{
                sh 'curl -o /dev/null --silent --head --write-out "%{http_code}\n" http://jenkins-udacity-mustafa.s3-website.us-east-2.amazonaws.com/'
            }
        }
    }
}