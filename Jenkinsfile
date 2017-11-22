node {
  try{

    stage 'checkout project'
    git url: 'https://github.com/rugaba/game-of-life.git'
    checkout scm

    stage 'check env'

    sh "mvn -v"
    sh "java -version"

    stage 'test'
    sh "mvn test"

    stage 'package'
    sh 'mvn -B -V -U -e clean package'


    stage 'report'
    junit allowEmptyResults: true, testResults: '**/target/surefire-report/*.xml'

    stage 'Artifact' 
    step([$class: 'ArtifactArchiver', artifacts: '**/target/*.jar', fingerprint: true])

  
    stage 'deploy'
    sh 'make deploy-default'


  }catch(e){
    
    throw e;
  }
}
