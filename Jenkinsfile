pipeline {
    agent any
    stages { 
        stage('build') {
            steps {
                echo 'Building..'
                sh 'javac -d . src/*.java'
                sh 'echo Main-Class: Rectangulator > MANIFEST.MF' 
                sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
            }
        }
        stage('Test') {
              steps {
                  echo 'Testing..'
              }
        }
        stage('Deploy') {
           steps {
              echo 'Deploying....'
           }
        }
        stage('run') {
           steps {
              sh 'java -jar rectangle.jar 7 9' 
           }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'rectangle.jar', fingerprint: true
        }
    }    
}
    // Script //
node {
    stage('Build') {
      echo 'Building....'
    }
    stage('Test') {
      echo 'Building....'
    }
    stage('Deploy') {
      echo 'Deploying....'
    } 
}
