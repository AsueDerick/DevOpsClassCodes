pipeline {
       
    tools {
        maven 'mymaven'
    }
    agent none
    stages {
        stage('Clonerepo') {
            agent any
            steps {
                git 'https://github.com/bhasker-manikyala/DevOpsClassCodes.git'
            }
        }
        stage('Compile') {
            agent any
            steps {
                sh 'mvn compile'
            }
        }
        stage(CodeReview) {
            agent any
            steps {
                sh 'mvn pmd:pmd'
            }
            post {
  success {
    recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
  }
}
        }
        stage(UnitTesting){
            agent any
            steps {
                sh 'mvn test'
            }
        }
        stage('Codecoverage'){
            agent any
            steps {
               sh 'mvn verify'   
            }
        }
        stage('Package'){
            agent any
            steps {
               sh 'mvn package'   
            }
        }
    }
}
