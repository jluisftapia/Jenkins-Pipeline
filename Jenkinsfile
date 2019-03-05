pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Server') {
          agent {
            docker {
              image 'maven:3.5-jdk-8-slim'
            }

          }
          steps {
            sh '''echo "Building the code for the server" 
mvn -version 
mkdir -p target 
touch "target/server.war"'''
            stash(name: 'server', includes: '**/*.war')
          }
        }
        stage('Client') {
          agent {
            docker {
              args '-u 0:0'
              image 'node'
            }

          }
          steps {
            sh '''echo "Building the code for  a client"
npm install --save react

mkdir -p dist cat > dist/index.html <<EOF 
Hello welcome to this pipeline practice made with jenkins and GitHub!!! 
EOF 
touch "dist/client.js"'''
          }
        }
      }
    }
  }
}