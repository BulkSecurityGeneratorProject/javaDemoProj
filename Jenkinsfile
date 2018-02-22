pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh '''JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.51-1.b16.el7_1.x86_64
export JAVA_HOME

M2_HOME=/home/moazzams/maven
export M2_HOME
M2=$M2_HOME/bin
export M2

PATH=$PATH:$JAVA_HOME
PATH=$PATH:$M2
export PATH
echo $PATH
mvn clean install -Pprod -DskipTests'''
          }
        }
        stage('Var') {
          steps {
            sh '''export PATH=$PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin
echo $PATH'''
          }
        }
      }
    }
    stage('Test') {
      steps {
        sh '''export M2_HOME=/opt/apache-maven-3.5.2
export M2=$M2_HOME/bin
export PATH=$M2:$PATH
mvn test'''
      }
    }
    stage('Deploy') {
      steps {
        cleanWs(cleanWhenSuccess: true)
      }
    }
  }
}