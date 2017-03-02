#!groovy
node {
   // Mark the code checkout 'stage'.... test2 Mar 2
   stage 'Git Checkout'

   // Get some code from a GitHub repository

   
   checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'PerBuildTag']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '146ff225-d9c5-4466-9ae0-3ff4c646ff30', url: 'https://github.com/snyamars/wcw_micro_salesorder.git']]]

   // Get the maven tool.
   // ** NOTE: This 'M3' maven tool must be configured
   // **       in the global configuration.           
   //def mvnHome = tool 'Maven'

   // Mark the code build 'stage'....
   stage 'Build'
   //set the version
   //sh "${mvnHome}/bin/mvn versions:set -DnewVersion=1.0.${env.BUILD_NUMBER}"
   // Run the maven build.
   
   //sh "${mvnHome}/bin/mvn release:update-versions -DautoVersionSubmodules=true"
   //sh "${mvnHome}/bin/mvn release:prepare"
  
  stage 'Update Nexus'
  
  //sh "${mvnHome}/bin/mvn clean package deploy"
  
  //sh "${mvnHome}/bin/mvn clean package"
  
   def fileName = "/var/lib/jenkins/workspace/${env.JOB_NAME}/<service name>"
   echo "$fileName"
  def word1 = "warfile=${fileName}"
  echo "${word1}"
  
 // def targetIPAddress = "${targetIPAddress}"
// echo "${targetIPAddress}"
  
  def tag_value = "${tag_value}"
  echo "${tag_value}"
  
  
  def artifactLocation ="/var/lib/jenkins/workspace/${env.JOB_NAME}/wcw_micro_salesorder"
  
  stage 'Git Tagging'
  
  withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '146ff225-d9c5-4466-9ae0-3ff4c646ff30', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD']]) 
  {
      //sh("git tag -a ${env.BUILD_NUMBER}  -m 'Jenkins'")
      sh("git tag -a wcw_micro_salesorder_${tag_value}_${env.BUILD_NUMBER}  -m 'Jenkins'")
      sh('git push https://"${GIT_USERNAME}":"${GIT_PASSWORD}"@github.com/snyamars/wcw_micro_salesorder.git --tags')
  }
  
stage 'docker build'
  
  docker.withRegistry('', 'f6ab1d37-c2cf-4636-80b9-7745dffd4695') {
        def pcImg = docker.build('snyamars007/node_salesorder')
        pcImg.push();
  }
  

 
 stage 'notifyKubernetes'
   //sh  "curl -H 'Content-Type: application/json' -X POST -d '{'id': 'wcw-sales','application': 'Warehouse-Application','accesspoint': 'http://172.31.0.233:8080','containers': [{'name': 'mongo', 'replicas': 1, 'cpu': 1100, 'memory': '170M', 'port': 30072},        {'name': 'node', 'replicas': 1, 'cpu': 1100, 'memory': '500M', 'port': 30065, 'image': 'snyamars007/node_salesorder'} ]}' http://54.237.219.53:3306/step3"
   //sh ('curl -H Content-Type: application/json -X POST -d "{  "id": "wcw-sales",     "application": "Warehouse-Application",     "accesspoint": "http://172.31.0.233:8080",     "containers": [         {"name": "mongo", "replicas": 1, "cpu": 1100, "memory": "170M", "port": 30072},         {"name": "node", "replicas": 1, "cpu": 1100, "memory": "500M", "port": 30065, "image": "snyamars007/node_salesorder"}  ] }" http://54.237.219.53:3306/step3')
   //sh ('curl -H Content-Type: application/json -X POST -d '{  "id": "wcw-sales",     "application": "Warehouse-Application",     "accesspoint": "http://172.31.0.233:8080",     "containers": [         {"name": "mongo", "replicas": 1, "cpu": 1100, "memory": "170M", "port": 30072},         {"name": "node", "replicas": 1, "cpu": 1100, "memory": "500M", "port": 30065, "image": "snyamars007/node_salesorder"}  ] }' http://54.237.219.53:3306/step3')
   //sh "curl -H Content-Type: application/json -X POST -d "'{  "id": "wcw-sales",     "application": "Warehouse-Application",     "accesspoint": "http://172.31.0.233:8080",     "containers": [         {"name": "mongo", "replicas": 1, "cpu": 1100, "memory": "170M", "port": 30072},         {"name": "node", "replicas": 1, "cpu": 1100, "memory": "500M", "port": 30065, "image": "snyamars007/node_salesorder"}  ] }'" http://54.237.219.53:3306/step3"
   //sh "curl -H 'Content-Type: application/json' -X POST -d "'{  "id": "wcw-sales",     "application": "Warehouse-Application",     "accesspoint": "http://172.31.0.233:8080",     "containers": [         {"name": "mongo", "replicas": 1, "cpu": 1100, "memory": "170M", "port": 30072},         {"name": "node", "replicas": 1, "cpu": 1100, "memory": "500M", "port": 30065, "image": "snyamars007/node_salesorder"}  ] }'" http://54.237.219.53:3306/step3"
   //sh "curl -H 'Content-Type: application/json' -X POST -d "{  "id": "wcw-sales",     "application": "Warehouse-Application",     "accesspoint": "http://172.31.0.233:8080",     "containers": [         {"name": "mongo", "replicas": 1, "cpu": 1100, "memory": "170M", "port": 30072},         {"name": "node", "replicas": 1, "cpu": 1100, "memory": "500M", "port": 30065, "image": "snyamars007/node_salesorder"}  ] }" http://54.237.219.53:3306/step3"
   //sh ('curl -H "Content-Type: application/json" -X POST -d '{  "id": "wcw-sales",     "application": "Warehouse-Application",     "accesspoint": "http://172.31.0.233:8080",     "containers": [         {"name": "mongo", "replicas": 1, "cpu": 1100, "memory": "170M", "port": 30072},         {"name": "node", "replicas": 1, "cpu": 1100, "memory": "500M", "port": 30065, "image": "snyamars007/node_salesorder"}  ] }' http://54.237.219.53:3306/step3')
   sh 'curl -vvv -X POST -d @salesFile -H "Content-Type: application/json" http://52.2.95.61:3306/step3'
}//end of node
