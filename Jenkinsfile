pipeline{
    agent any
    environment{
        staging_server="192.168.5.40"
    }
    stages{
        stage('Deploy to Remote'){
            steps{
                sh '''
                    for fileName in `find ${WORKSPACE} -type f -mmin -10 | grep -v ".git" | grep -v "Jenkinsfile"`
                    do
                        fil=$(echo ${fileName} | sed 's/'"${JOB_NAME}"'/ /' | awk {'print $2'})
                        scp -r ${WORKSPACE}${fil} k8@${staging_server} -P 1524:/var/www/html/cicd${fil}
                    done
                '''
            }
        }
    }
}