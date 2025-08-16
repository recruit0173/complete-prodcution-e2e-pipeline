pipeline 
{

agent {
  label 'server1'
}

tools {
  maven 'mymaven'
}

environment {
  NAME = "moninderr"
}


parameters {
  choice choices: ['dev', 'prod'], name: 'select_environment'
}

stages{

    stage('build'){
        steps {
            sh 'mvn clean package -DskipTests=true'
            echo "hello $NAME ${params.LASTNAME}"
        }

        

    }

    stage('test')
    {
      parallel {
        stage('testA')
        {
          agent { label 'server1'}
          steps{
            echo "this is test A"
            sh "mvn test"
          }
        }
        stage('testB')
        { 
          agent { label 'server1'}
          steps{
            echo "this is testB"
            sh "mvn test"
          }
        }
        stage("sonarqube analysis"){
          steps {
            withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
            echo "sonarqube analysis"
            sh "mvn sonar:sonar"
          }
        }
      }
      post {
        success {
            archiveArtifacts artifacts: '**/target/*.jar'
                    }
        }
    }

    
}

}