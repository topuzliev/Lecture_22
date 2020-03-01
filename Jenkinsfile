def appName="my-app"
def appVersion="1.0-SNAPSHOT"

node('dockerslave'){
    tool name: 'maven', type: 'maven'
    stage('Check prerequest'){
        withEnv(["PATH=${env.PATH}:${tool 'maven'}/bin"]){
        sh 'env | grep PATH'
        echo "${tool 'maven'}"
        sh 'mvn -v'
 //       withMaven
    }
    stage('Get source'){
        git branch: 'master',
        url: 'https://github.com/jenkins-docs/simple-java-maven-app.git'
    }
    stage('Build') {
         
                withEnv(["PATH=${env.PATH}:${tool 'maven'}/bin"]){
                sh 'mvn -B -DskipTests clean package'
 //               appName = sh (script: "mvn help:evaluate -Dexpression=project.name | grep -v \"[\"", returnStdout: true).trim()
  //              appVersion = sh (script: "mvn help:evaluate -Dexpression=project.version | grep grep -v \"[\"", returnStdout: true).trim()
            }
        }
            stage('Test') {
          
                withEnv(["PATH=${env.PATH}:${tool 'maven'}/bin"]){
                sh 'mvn test'
                stash include: 'taregt/my-app-1.0-SNAPSHOT.jar', name: 'artifactStash'
           
            }
        }
}
}
node('dockerslave1'){
    tool name: 'Docker', type: 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
    
    stage('Check prerequest'){
        echo "${tool 'Docker'}"
        sh 'ls -lah'
        withEnv(["PATH=${env.PATH}:${tool 'Docker'}/bin"]){
        sh 'docker -v'
            }
            
        stage('Get Dockerfile'){
            git(url: 'git@github.com:topuzliev/Lecture_22.git', branch: "master", credentialsId: 'Privet')
 //           git branch: 'master',
 //           url: 'https://github.com/topuzliev/Lecture_22.git'
            } 

        stage('unstash our application'){
            unstash 'artifactStash'
            } 
            
        stage('Build Dockerfile'){
            withEnv(["PATH=${env.PATH}:${tool 'Docker'}/bin"]){
            sh "docker build --no-cache --build-arg APP_NAME=${appName} --build-arg APP_VERSION=${appVersion} -t myappdocker ."
            sh "docker images"
 //           sh "docker build --no-cache --build-arg APP_NAME=${appName} --build-arg APP_VERSION=${appVersion} -t myappdocker"
            } 
    }

    stage('Push image'){
        withEnv(["PATH=${env.PATH}:${tool 'Docker'}/bin"]){
            withDockerRegistry(credentialsId: 'dockerhub', url: 'https://index.docker.io/v1/topuzliev'){
                sh "docker push myappdocker:latest"
                sh "docker -v"
                sh "docker images"
                
            }
    }
    }
    }
}
    






/*pipeline {
    agent {
        docker {
            image 'maven'
            args '-v ~/.m2:/var/maven/.m2'
            //            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
*/