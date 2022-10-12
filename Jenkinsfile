pipeline {
    agent none
    tools{
       jdk 'My_JAVA_Maven'
       maven 'My_Maven'

    }
        stages {
         stage('Compile') {
             agent any
            steps {
            script {
                echo "Compiling the code"
                sh 'mvn compile'
            }       
            }
        }
        stage('UnitTest') {
            agent {label 'Linux_Slave_2'}
            steps {
                script{
                    echo "Running the Test Cases"
                    sh 'mvn test' 
            }
            }
        post{
            always{
                junit 'target/surefire-reports/*.xml'
            }
        }    
        }    
        stage('Package') {    
            agent any
             steps{
                script {
                    echo "Packaging the Code"
                    sshagent(['Build_Server_Key']) {
                    sh "scp -o StrictHostKeyChecking=no server-script.sh ec2-user@65.2.148.234: /home/ec2-user"
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@65.2.148.234 'bash ~/server-script.sh"
                    sh 'mvn package'
                }
    
            }
        }
    }
}
}