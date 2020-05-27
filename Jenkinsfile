pipeline {
   agent any

   stages {
      stage('拉取代码') {
         steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'b85634f8-4e1a-423d-8269-cb65a506900b', url: 'https://github.com/993034494/web_demo.git']]])
         }
      }
      stage('编译打包') {
         steps {
            sh label: '', script: '/usr/local/apache-maven-3.6.2/bin/mvn clean package'
         }
      }
      stage('远程发布') {
         steps {
            deploy adapters: [tomcat8(credentialsId: '6cf2b312-3072-454b-94b3-79326cc9b7bb', path: '', url: 'http://192.168.100.103:8080/')], contextPath: null, war: 'target/*.war'
         }
      }
   }
}

