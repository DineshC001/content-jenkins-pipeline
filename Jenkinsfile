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
              if (currentBuild.result == null || currentBuild.result == 'SUCCESS') { 
                 sh 'make publish'
              }
           }
        }
        stage('run') {
           steps {
              /* `make check` returns non-zero on test failures,
              * using `true` to allow the Pipeline to continue nonetheless
              */
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
      sh 'javac -d . src/*.java'
      sh 'echo Main-Class: Rectangulator > MANIFEST.MF'
      sh 'jar -cvmf MANIFEST.MF rectangle.jar *.class'
    }
    stage('Test') {
      echo 'Building....'
      /* `make check` returns non-zero on test failures,
      * using `true` to allow the Pipeline to continue nonetheless 
      */
      sh 'java -jar rectangle.jar 7 9'
    }
    stage('Deploy') {
      echo 'Deploying....'
      if (currentBuild.result == null || currentBuild.result == 'SUCCESS') { 
         sh 'make publish'
      }
    } 
}
