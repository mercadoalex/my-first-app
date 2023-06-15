node {
    stage('Checkout'){
        checkout scm  
    } 
    stage('NPM Install'){
        sh 'sudo apt update'
        sh 'sudo apt upgrade'
        //sh 'sudo apt install nodejs'
        //sh 'sudo apt install npm'
        sh 'sudo apt install nodejs npm -y'
        sh 'node -v'
        sh 'npm -v'
        sh 'npm install -g @angular/cli'
        sh 'ng --version'
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
        sh 'ls'
    } 
    stage('Deploy'){
        echo 'Deploy - no hay servidor aun'
    }
}
