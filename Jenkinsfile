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
                    retry(2) {
                        s3Upload(bucket:"jenkins-udacity-mustafa", path:'', includePathPattern:'*.html')
                    }
                }
            }
        }
        stage('Validate deployment'){
            steps{
                sh '''
                    response=$(curl -s -o /dev/null -w "%{http_code}\n" http://jenkins-udacity-mustafa.s3-website.us-east-2.amazonaws.com/)
                    if [ "$response" != "200" ]
                    then
                        exit 1
                    fi
                '''
            }
        }
    }
}