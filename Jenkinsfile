pipeline{
  agent any
  options { timestamps () }
  stages{

    stage('Building_UAT_Package'){
      steps{
        sh 'mvn -f java-tomcat-sample/pom.xml clean package'
      }

      post {
        success{
          echo "Artifacts has been created...Archiving it"
          archiveArtifacts artifacts: '**/*.war'
        }
      }
    }

    stage('UAT_Deployment'){
      steps{
      copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, flatten: true, projectName: 'Pipeline_Package_Creation_Deployment', target: '/opt/tomcat/staging'
      echo "Artifacts copied to Staging"
        
        sh '''
          set +x
          sudo /opt/tomcat/apache-tomcat-9.0.53_prod/bin/shutdown.sh
          sudo rm -rf /opt/tomcat/apache-tomcat-9.0.53_prod/webapps/UAT/
          sudo rm -rf /opt/tomcat/apache-tomcat-9.0.53_prod/webapps/UAT.war
          mv /opt/tomcat/staging/java-tomcat-maven-example.war /opt/tomcat/apache-tomcat-9.0.53_prod/webapps/UAT.war
          echo "Deployed to UAT"
          sudo /opt/tomcat/apache-tomcat-9.0.53_prod/bin/startup.sh
        '''
      }
    }

    stage('Production Deployment'){
      agent { label 'jenkins_slave_1' }
      steps{
        timeout(2){
          input message: "Proceed to Production?"
        }
        
         copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, flatten: true, projectName: 'Pipeline_Package_Creation_Deployment', target: '/opt/apache/production_artifacts/'
      echo "Artifacts copied to Production"
        
        sh '''
          set +x
          sudo /opt/apache/apache-tomcat-9.0.54/bin/shutdown.sh
          sudo rm -rf /opt/apache/apache-tomcat-9.0.54/webapps/PROD/
          sudo rm -rf /opt/apache/apache-tomcat-9.0.54/webapps/PROD.war
          mv /opt/apache/production_artifacts/java-tomcat-maven-example.war /opt/apache/apache-tomcat-9.0.54/webapps/PROD.war
          echo "Deployed to PROD"
          sudo /opt/apache/apache-tomcat-9.0.54/bin/startup.sh
        '''
        
      }
    }

  }
}
