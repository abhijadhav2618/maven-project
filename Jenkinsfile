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

            stage("deploy the application on apache"){
                steps{
                    sshagent(['DEVCICD']) {
                           sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.13.128:/usr/share/tomcat/webapps'
                    }
                }
            }
        
    }
}
