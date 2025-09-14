// use of scripted pipeline in jenkins file for the awsec2 deployment

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
            url: 'https://github.com/Rabin-Mishra/ci-cd-jenkins-awsec2-github-webook-nextjs.git'
        )
    }

    stage('Deploy to EC2'){
        echo 'Deploying to EC2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}
            sudo npm install
            sudo npm run build
            sudo fuser -k 3000/tcp || true
            npm run start
        """
    }
}