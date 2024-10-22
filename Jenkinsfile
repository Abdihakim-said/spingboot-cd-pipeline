pipeline {
  agent any
 //agent { label 'build' }
 parameters {
     password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Gitlab password')
     string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
 }

    stages {
        stage('Deploy') {
            steps {
                script {
                    git branch: 'main', credentialsId: 'GitlabCred', url: 'https://gitlab.com/wezva1312328/spingboot-cd-pipeline.git'
                    
                    dir("./kubernetes") {
                        sh "sed -i 's/image: abdihakimdevops.*/image: abdihakimdevops\\/wezvatechbackend:$IMAGETAG/g' deployment.yml"
                    }
                    
                    sh 'git commit -a -m "New deployment for Build $IMAGETAG"'
                    
                    withCredentials([string(credentialsId: 'gitlab_token', variable: 'GITLAB_TOKEN')]) {
                        sh "git push https://abdihakimsaid1:$GITLAB_TOKEN@gitlab.com/wezva1312328/spingboot-cd-pipeline.git"
                    }
                }
            }
        }
    }
}
