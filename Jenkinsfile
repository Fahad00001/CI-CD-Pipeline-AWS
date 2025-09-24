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

//  stage('Deploy to EC2'){
//     echo 'Deploying to EC2'
//     bat """
//         mkdir %appDir%
//         xcopy * %appDir% /E /Y /I
//         cd %appDir%
//         call npm install
//         call npm run build
//         taskkill /F /IM node.exe || echo No process found
//         start /B npm run start
//     """
// }

stage('Deploy to EC2') {
    echo 'Deploying to EC2'
    bat """
        REM Create app directory
        if not exist %appDir% mkdir %appDir%
        
        REM Copy files (exclude node_modules and .git)
        xcopy /E /I /Y . %appDir%\\
        
        REM Move to app directory
        cd %appDir%
        
        REM Install dependencies
        call npm install
        
        REM Build Next.js app
        call npm run build
        
        REM Kill Node process if running on port 3000
        for /f "tokens=5" %%a in ('netstat -a -n -o ^| findstr :3000 ^| findstr LISTENING') do taskkill /F /PID %%a
        
        REM Start the Next.js app
        start /B npm run start
    """
}

}