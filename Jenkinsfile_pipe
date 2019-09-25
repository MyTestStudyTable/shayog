pipeline {
    
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package'
                sh 'mvn site'
                sh 'mvn site-deploy'
            }
        }
    }
}
