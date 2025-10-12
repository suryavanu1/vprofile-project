pipeline {
    agent any
    tools {
        maven "MAVEN3.9"
        jdk "JDK17"
    }
    
    environment {
        SNAP_REPO = 'vprofile-snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'admin123'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '172.31.14.192'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now archiving the artifacts..."
                    archiveArtifacts artifacts: '**/*.war'
                    
                }
                
            }
        }
        stage('Test'){
            steps {
                sh 'mvn test'
            }
        }
        stage('Checkstyle'){
            steps {
                sh 'mvn checkstyle:checkstyle'
                
            }
        }
    }
}