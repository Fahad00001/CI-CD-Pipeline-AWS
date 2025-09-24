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

// stage('Deploy to EC2') {
//     echo 'Deploying to EC2'
//     bat """
//         mkdir "${appDir}"
//         xcopy /E /Y /I . "${appDir}\\"
//         cd "${appDir}"
//         call npm install
//         call npm run build
//         for /f "tokens=5" %%a in ('netstat -a -n -o ^| findstr :3000 ^| findstr LISTENING') do taskkill /F /PID %%a
//         start /B npm run start
//     """
// }

stage('Deploy to EC2'){
    echo 'Deploying to EC2'
    bat """
        REM Set app directory
        set appDir=C:\\var\\www\\nextjs-app

        REM Create app directory
        if not exist %appDir% mkdir %appDir%

        REM Copy files to app directory
        xcopy * %appDir% /E /Y /I

        REM Go to app directory
        cd %appDir%

        REM Install dependencies
        call npm install

        REM Build the Next.js app
        call npm run build

        REM Kill any existing Node process on 3000
        taskkill /F /IM node.exe || echo No process found

        REM Start app in background accessible publicly
        start /B npm run start -- -H 0.0.0.0 -p 3000
    """
}


}