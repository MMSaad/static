pipeline {
    agent any
    stages {
        stage('Upload to AWS'){
            steps{
                withAWS(region:'us-east-2',credentials:'Jenkins') {
                    s3Upload(file:'index.html', bucket:'jenkins-udacity-mustafa', path:'index.html')
                }
            }
        }
    }
}