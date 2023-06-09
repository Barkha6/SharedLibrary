@Library("shared-library") _
pipeline {
    agent {
        label 'Built-In Node'
    }
    stages {
	stage('Git Check Out') {
            steps {
           	gitCheckOut(
                    branch: "main",
                    url: "https://github.com/Barkha6/SharedLibrary.git"
                )
            }
        }
        stage('BuildMavenJar') {
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
        /*stage('SonarScan') {
            steps {
                withSonarQubeEnv('sq1') {
                    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar'
                }
            }
        }*/
        stage('Deliver-executeJava') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
        /*stage("Publish to Nexus") {
            steps {
                script {
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: 'nexus3',
                            protocol: 'http',
                            nexusUrl: '65.0.128.192:8081',
                            groupId: 'pom.com.mycompany.app',
                            version: 'pom.4.0-SNAPSHOT',
                            repository: 'maven-central-repository',
                            credentialsId: 'NEXUS_CRED',
                            artifacts: [
                                [artifactId: 'pom.my-app',
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
                }
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t ranjanvivek/hello-world .'
                }
            }
        }
        stage('Push image to DockerHub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u ranjanvivek -p ${dockerhubpwd}'
                   }
                   sh 'docker push ranjanvivek/hello-world'
                }
            }
        }
        /*stage('Pull image and run container'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u ranjanvivek -p ${dockerhubpwd}'
                   }
                   //sh 'docker pull ranjanvivek/devops-integration'
                   sh 'docker container run -d --name=app1 ranjanvivek/hello-world'
                }
            }
        } */
        /*stage('Deploy App on k8s') {
		    steps {
			    sshagent(['k8s']) {
				    sh "scp -o StrictHostKeyChecking=no deploymentservice2.yaml ubuntu@65.0.55.243:/home/ubuntu"
				    script {
					    try{
						    sh "ssh ubuntu@65.0.55.243 kubectl create -f ./deploymentservice2.yaml"
					    }catch(error){
						    sh "ssh ubuntu@65.0.55.243 kubectl apply -f ./deploymentservice2.yaml"
					    }
				    }
			    }  
		    }
	    }*/
	stage( 'SharedLibraryExample') {
		steps {
			helloAll()
			helloDay("All","2nd June")
			helloWorld(name:"All",dayOfWeek:"Friday")
			helloWorld(dayOfWeek:"Friday",name:"Team")
		}
	}
    }
}
