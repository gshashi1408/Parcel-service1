pipeline {
  agent {
    label 'slave2'
  }
  stages {
    stage('checkout') {
      steps {
        sh 'rm -rf parcel-service'
        sh 'git clone https://github.com/gshashi1408/Parcel-service1.git'
      }
    }
    stage('build') {
      steps {
        sh 'mvn clean install'
      }
    }
        stage('Run Locally') {
            steps {
                script {
                    sh "java -jar target/simple-parcel-service-app-1.0-SNAPSHOT.jar &"
                    sleep 30
                }
            }       
        stage('deploy') {
            steps {
                sh 'ssh root@172.31.37.35'
                sh "scp /home/slave2/workspace/parcelservice_feature-1/target/simple-parcel-service-app-1.0-SNAPSHOT.jar root@172.31.37.35:/root/apache-tomcat-8.5.98/webapps"
            }
        }      
    }      
}
}
