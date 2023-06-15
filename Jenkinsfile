//groovy
properties(
    [
        [$class: 'BuildDiscarderProperty', strategy:
            [$class: 'LogRotator', artifactDaystoKeepStr: '14',artifactNumToKeepStr:'5', daysToKeepStr: '30', numToKeepStr: '60']],
        pipelineTriggers(
            [
                pollSCM('H/15 * * * *'),
                cron('@daily'),
            ]
        )     
        ]
) 
node {
    stage('Checkout'){
        //github
        //workspace
        deleteDir()
        checkout scm  
    } 
    stage('NPM Install'){
        sh 'npm install'
    }
    stage('Test'){
        withEnv(["CHROME_BIN=/usr/bin/chromium-browser"]){
            sh 'ng test --progress=false --watch=false'
        }
        junit '**/test-results.xml'
    }
    stage('Lint - ESLint'){
        sh 'ng lint'
    } 
    stage('Build'){
        sh 'ng build --prod --aot --sm --progress=false' 
    } 
    stage('Archive'){
        sh 'tar -cvzf dist.tar.gz --strip-components=1 dist'
        archive 'dist.tar.gz'
    } 
    stage('Deploy'){
        echo 'Deploy'
    }
}
