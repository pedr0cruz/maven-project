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
    string(name: 'tomcat_dev', defaultValue: '192.168.1.31:8080', description: 'Staging Server')
    string(name: 'tomcat_prod', defaultValue: '192.168.1.31:9090', description: 'Production Server')
  }
  triggers {
    pollSCM('* * * * *')
  }
}
