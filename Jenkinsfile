pipeline{
 agent {label 'dev-server'}  
 triggers {
        pollSCM '* * * * *'
    }
    stages{
        stage('checkout'){
            steps{
              checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '53008af3-fa93-46c3-bc00-84ec7206ba53', url: 'https://github.com/dinesh-annexit/mavenrepo.git']]])  
            }
        }
        stage('build'){
            steps{
                sh 'mvn package'
            }
        }
          stage('sonar'){
            steps{
                withSonarQubeEnv('mysonar') {
sh 'mvn sonar:sonar'
}
                
            }
        }
        
        stage('nexus'){
            steps{
                sh 'mvn deploy'
            }
        }
        
        stage('tomcat'){
            steps{
                sh 'scp /root/workspace/sample/target/studentapp-2.5-SNAPSHOT.war root@43.205.207.55:/var/lib/tomcat/webapps'
            }
        }
        
    }
}
