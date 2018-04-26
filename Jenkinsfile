node {

    withMaven(maven:'maven') {

        stage('Checkout') {
            git url: 'https://github.com/NaveenGShephertz/discovery-service.git', credentialsId: 'naveengshephertz', branch: 'master'
        }

        stage('Build') {
            sh 'mvn clean install'

            def pom = readMavenPom file:'pom.xml'
            print pom.version
            env.version = pom.version
        }

        stage('Image') {
                def app = docker.build "discovery-service:latest"
        }

        stage ('Run') {
				sh 'docker stack deploy -c docker-compose.yml discovery-service'
        }

    }

}