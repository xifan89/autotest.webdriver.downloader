node {
  def mvnHome
  stage('Preparation') {
    git 'https://github.com/LinuxSuRen/autotest.webdriver.downloader.git'
    mvnHome = tool 'M3'
  }
  
  stage('Build') {
    if(isUnix()){
      sh "'${mvnHome}/bin/mvn' clean package"
    }else{
      bat(/"${mvnHome}\bin\mvn" clean package/)
    }
  }
  
  stage('Deploy') {
    if(isUnix()){
      sh "'${mvnHome}/bin/mvn' deploy -DsignSkip=false -DdocSkip=false"
    }else{
      bat(/"${mvnHome}\bin\mvn" deploy -DsignSkip=false -DdocSkip=false/)
    }
  }
}

properties([
    [
        $class: 'GithubProjectProperty',
        displayName: 'autotest.webdriver.downloader',
        projectUrlStr: 'https://github.com/LinuxSuRen/autotest.webdriver.downloader'
    ],
    buildDiscarder(
        logRotator(
            artifactDaysToKeepStr: '',
            artifactNumToKeepStr: '',
            daysToKeepStr: '7',
            numToKeepStr: '14'
        )
    ),
    pipelineTriggers([
        pollSCM('H/15 * * * *')
    ])
])