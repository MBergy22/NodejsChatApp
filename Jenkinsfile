node('App-Server-CWEB2140')
{
    def app
    stage('CLONE GIT REPOSITORY')
    {
        // Let's make sure we have the repository cloned to our workspace
        checkout scm

    }
    stage('SCA-SAST-SYNK-TEST')
    {
        snykSecurity(
            snykInstallation: 'Snyk-Latest',
            snykTokenId: 'Snyk_ID',
            severity: 'critical'
            )

    }


    stage('BUILD-AND-TAG')
    {
        app = docker.build('bermics/chatapphw')

    }

    stage('POST-TO-DOCKERHUB')
    {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
        {
          app.push("latest")
        }


    }
    stage('DEPLOYMENT')
    {
        sh "docker-compose down"
        sh "docker-compose up -d"

    }
}
