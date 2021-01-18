pipeline {
agent any 
tools {
('maven')
 }
stages  {
stages ('initialize') {
 steps { 
 sh '''
   "echo "$PATH = ${PATH}"
   "echo "$M2_HOME = ${M2_HOME}"
   '''
    }
  }
  stage ('build'){
   sh 'mvn clean package'
    }   
    
  }
}

