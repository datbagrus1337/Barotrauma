pipeline {
  agent {
    node {
      label 'agent1'
    }

  }
  stages {
    stage('File Check') {
      steps {
        sh '''ls -la
'''
      }
    }

    stage('SDL Controller Map Patch') {
      steps {
        sh '''mkdir -p Libraries/MonoGame.Framework/Src/ThirdParty/SDL_GameControllerDB
wget https://raw.githubusercontent.com/gabomdq/SDL_GameControllerDB/master/gamecontrollerdb.txt -O Libraries/MonoGame.Framework/Src/ThirdParty/SDL_GameControllerDB/gamecontrollerdb.txt'''
      }
    }

    stage('Build Client') {
      parallel {
        stage('Build Client') {
          steps {
            sh 'dotnet publish Barotrauma/BarotraumaClient/LinuxClient.csproj --configuration Release --self-contained --runtime linux-x64 /p:Platform=x64 /p:DebugType=None --output game'
          }
        }

        stage('Build Server') {
          steps {
            sh 'dotnet publish Barotrauma/BarotraumaServer/LinuxServer.csproj --configuration Release --self-contained --runtime linux-x64 /p:Platform=x64 /p:DebugType=None --output game'
          }
        }

      }
    }

    stage('Write output') {
      steps {
        sh 'ls -la ./game'
      }
    }

  }
}