node {
   def mvnHome
  stage('Prepare') {
      git url: 'https://github.com/mallikarjunbhumi/sonar-code-jenkins.git', branch: 'main'
      mvnHome = tool 'maven'
  }

  stage ('Clean') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean -DskipTests"
  }
  stage ('Validate') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore validate"
  }
  stage ('Compile') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore compile"
  }
  stage ('Test') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore test"
  }
  stage ('Package') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore package"
  }
  stage ('Verify') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore verify"
  }
  stage ('Install') {
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore install"
  }
  stage ('Deliver & Deployment') {
      sh 'curl -u admin:redhat@123 -T target/**.war "http://13.233.128.154:8080/manager/text/deploy?path=/malli&update=true"'
  }
  stage ('SmokeTest') {
      sh 'curl --retry-delay 10 --retry 5 "http://13.233.128.154:8080/malli"'
  }
}
