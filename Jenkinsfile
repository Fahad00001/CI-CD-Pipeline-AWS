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
    sh """
        mkdir -p ${appDir}
        rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}
        cd ${appDir}
        /usr/bin/npm install
        /usr/bin/npm run build
        fuser -k 3000/tcp || true
        nohup /usr/bin/npm start &
    """
}

}