pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven3'       // Make sure you configure Maven in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh '${MAVEN_HOME}/bin/mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh '${MAVEN_HOME}/bin/mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                sh '${MAVEN_HOME}/bin/mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add deployment steps here (e.g., Docker, K8s, SCP to a server)
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Check logs for details.'
        }
    }
}


























// pipeline {
//     agent any

//     tools{
//         jdk 'jdk17'
//         maven 'maven3'
//     }

//     stages {
//         stage('Code Checkout') {
//             steps {
//                 git branch: 'main', changelog: false, poll: false, url: 'https://github.com/AbderrahmaneOd/Spring-Boot-Jenkins-CI-CD'
//             }
//         }
        
//         stage('OWASP Dependency Check'){
//             steps{
//                 dependencyCheck additionalArguments: '--scan ./ --format HTML ', odcInstallation: 'db-check'
//                 dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
//             }
//         }

//         stage('Sonarqube Analysis') {
//             steps {
//                 sh ''' mvn sonar:sonar \
//                     -Dsonar.host.url=http://localhost:9000/ \
//                     -Dsonar.login=squ_9bd7c664e4941bd4e7670a88ed93d68af40b42a3 '''
//             }
//         }

//         stage('Clean & Package'){
//             steps{
//                 sh "mvn clean package -DskipTests"
//             }
//         }


        
//        stage("Docker Build & Push"){
//             steps{
//                 script{
//                     withDockerRegistry(credentialsId: 'DockerHub-Token', toolName: 'docker') {
//                         def imageName = "spring-boot-prof-management"
//                         def buildTag = "${imageName}:${BUILD_NUMBER}"
//                         def latestTag = "${imageName}:latest"  // Define latest tag
                        
//                         sh "docker build -t ${imageName} -f Dockerfile.final ."
//                         sh "docker tag ${imageName} abdeod/${buildTag}"
//                         sh "docker tag ${imageName} abdeod/${latestTag}"  // Tag with latest
//                         sh "docker push abdeod/${buildTag}"
//                         sh "docker push abdeod/${latestTag}"  // Push latest tag
//                         env.BUILD_TAG = buildTag
//                     }
                        
//                 }
//             }
//         }
        
//         stage('Vulnerability scanning'){
//             steps{
//                 sh " trivy image abdeod/${buildTag}"
//             }
//         }

//         stage("Staging"){
//             steps{
//                 sh 'docker-compose up -d'
//             }
//         }
//     }
// }
