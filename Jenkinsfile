pipeline{
    agent any
        stages{
            stage("SCM checkout"){
                steps{
                    git url:'https://github.com/abhijadhav2618/maven-project.git', branch:'master'
                }
            }

            stage("Maven compile"){
                steps{
                    withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                        sh "mvn compile"
                    }
                }
            }

            stage("Maven test"){
                steps{
                    withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                        sh "mvn test"
                    }
                }
            }

            stage("Maven build"){
                steps{
                    withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                        sh "mvn clean package"
                    }
                }
            }

            stage("docker build"){
                steps{
                    sh "docker build -t abhijadhav2618/docker923:latest ."
                }
            }

            stage("Push image to docker hub"){
                steps{
                    withDockerRegistry(credentialsId: 'Docker_Hub_Cred', url:"https://index.docker.io/v1/") {
                        sh "docker push abhijadhav2618/docker923:latest"

                    }   
                }
            }
        
    }
}
