node {

    withMaven(maven:'maven') {

        stage('Checkout') {
            git url: 'https://github.com/piomin/sample-spring-microservices.git', credentialsId: 'github-piomin', branch: 'master'
        }

        stage('Build') {
            sh 'mvn clean install'

            def pom = readMavenPom file:'pom.xml'
            print pom.version
            env.version = pom.version
        }

        stage('Image') {
            dir ('discovery-service') {
                def app = docker.build "discovery-service:latest"
                
            }
        }

//        stage ('Run') {
//            docker.image("discovery-service:latest").run('-p 8761:8761 -h discovery --name discovery')
//        }

//        stage ('Final') {
//            build job: 'account-service', wait: false
//        }      

    }

}