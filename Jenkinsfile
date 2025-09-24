node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo'){
        echo 'Cloning the repo'
        git(
            branch: 'main',
            url: 'https://github.com/Fahad00001/CI-CD-Pipeline-AWS'
        )
    }

 stage('Deploy to EC2'){
    echo 'Deploying to EC2'
    bat """
        mkdir %appDir%
        xcopy * %appDir% /E /Y /I
        cd %appDir%
        call npm install
        call npm run build
        taskkill /F /IM node.exe || echo No process found
        start /B npm run start
    """
}


}