pipeline{

    agent any

    tools{
       maven 'Maven 3.8.5' 
    }
    

    stages{
        stage('build'){
            steps{
                echo 'Compiling...'
                sh 'mvn compile'
            }
        }
        stage('test'){
            steps{
                echo 'Running unit tests...'
                sh 'mvn clean test'
            }
        }
        stage('package'){
            steps{
                echo 'Generating artifact...'
                sh 'mvn package -DskipTests'
            }
        }
    }
    
    post{
        always{
            echo 'this pipeline has completed...'
        }
        
    }
    
}
