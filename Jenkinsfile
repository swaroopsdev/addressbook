pipeline {
    agent none
    tools{
       jdk 'My_JAVA_Maven'
       maven 'My_Maven'
    }   
    environment{
        Build_Server_IP="ec2-user@65.2.148.234"
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
             steps {
                script {
                    echo "Packaging the Code"
                    sshagent(['Build_Server_Key']) {
                    sh "scp -o StrictHostKeyChecking=no server-script.sh ${Build_Server_IP}:/home/ec2-user"
                    sh "ssh -o StrictHostKeyChecking=no ${Build_Server_IP} 'bash ~/server-script.sh'"
                    sh 'mvn package'
                }
    
            }
        }
    }
}
}