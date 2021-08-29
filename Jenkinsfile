pipeline {
  agent any
  stages {
    stage('Build') {
      post {
        success {
          echo 'Now Archiving...'
          archiveArtifacts '**/target/*.war'
        }

      }
      steps {
        sh 'mvn clean package'
      }
    }

    stage('UAT') {
      parallel {
        stage('UAT') {
          steps {
            echo 'Pruebas integrales'
          }
        }

        stage('SC') {
          steps {
            echo 'Verificacion de codigo'
          }
        }

      }
    }

    stage('PRD') {
      steps {
        echo 'Despliegue a produccion'
      }
    }

  }
  parameters {
    string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
    string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
  }
  triggers {
    pollSCM('* * * * *')
  }
}