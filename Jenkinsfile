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

stage('Deploy to EC2') {
    echo 'Deploying to EC2'
    bat """
        mkdir "${appDir}"
        xcopy /E /Y /I . "${appDir}\\"
        cd "${appDir}"
        call npm install
        call npm run build
        for /f "tokens=5" %%a in ('netstat -a -n -o ^| findstr :3000 ^| findstr LISTENING') do taskkill /F /PID %%a
        start /B npm run start
    """
}



}