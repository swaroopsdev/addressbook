pipeline {
    agent any
    tools{
       jdk 'My_JAVA_Maven'
       maven 'My_Maven'

    }
        stages {
         stage('Compile') {
            steps {
            script {
                echo "Compiling the code"
                sh 'mvn compile'
            }       
            }
        }
        stage('UnitTest') {
            steps {
                script{
                    echo "Running the Test Cases"
                    sh 'mvn test' 
            }
            }
        }    
        stage('Package') {    
             steps{
                script {
                    echo "Packaging the Code"
                    sh 'mvn package'
                }
    
            }
        }
    }
}
