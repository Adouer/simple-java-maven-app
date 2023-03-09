pipeline {
  agent {
    docker {
      image 'maven:latest'
      args '-v /root/.m2:/root/.m2'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }

    stage('Test') {
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }

      }
      steps {
        sh 'mvn test'
      }
    }

    stage('Deliver') {
      steps {
        sh 'sh mvn -Dmaven.aliyun.repository=http://maven.aliyun.com/nexus/content/groups/public/ clean install'
        sh './jenkins/scripts/deliver.sh'
      }
    }
  }
}