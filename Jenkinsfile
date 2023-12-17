pipeline {
    agent any
    
    stages {
        stage("checkout"){
            steps {
                git branch: 'main', url: 'https://github.com/ebirdyx/jgsu-spring-petclinic.git'
            }
        }
        
        stage("build"){
            steps {
                sh "./mvnw package"
            }
        }
    
        stage("capture"){
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
                jacoco()
                junit '**/target/surefire-reports/TEST*.xml'
            }
        }
    }
    
    post {
        always { 
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
                to: 'ef@yahoo.com',
                recipientProviders: [previous()],
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_URL}]"
        }
    }
    
}
