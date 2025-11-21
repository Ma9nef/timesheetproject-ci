pipeline {

    agent any

    tools {
        // Ces outils doivent être configurés dans Jenkins -> Global Tool Configuration
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/hwafa/timesheetproject.git'
            }
        }

        stage('Build & Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Package - Build JAR') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Build & Packaging successful ! Le livrable JAR est prêt."
        }
        failure {
            echo "❌ Build failed. Vérifie les logs Maven."
        }
    }
}
