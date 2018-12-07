pipeline {
    agent any
    stages {
        stage('Limpiar Workspace') {
            steps {
               cleanWs()
            }
        }
        stage('Obtener Fuentes Git') {
            steps {
                git branch: 'dev', credentialsId: '56d5fd04-205b-40f4-a270-45b2ea28f916', url: 'https://github.com/sw-hcm-dl/hcm.git'
                
            }
        }
        stage('Restaurar paquetes Nuget') {
            steps {
                bat 'C:\\nuget\\nuget.exe restore D:\\workspace\\Dev_Pip_Hcm\\DL.sln'
            }
        }
        stage('Limpiar Solucion') {
            steps {
                bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Community\\MSBuild\\15.0\\Bin\\MSBuild.exe" DL.sln /t:clean'
            }
                
        }
        stage('Compilar y Desplegar Proyecto') {
            steps {
                bat '"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Community\\MSBuild\\15.0\\Bin\\MSBuild.exe" DL.sln /p:DeployOnBuild=True /p:PublishProfile=dev.pubxml'
            }
        }
        stage('Eliminando Archivos de Configuración') {
            steps {
                //fileOperations([fileDeleteOperation(includes: '**/*.config', excludes: '')])
                bat 'if exist "D:\\deploy\\HCM\\temp" RMDIR /Q /S "D:\\deploy\\HCM\\temp"'
                bat 'if exist "D:\\deploy\\HCM\\logs" RMDIR /Q /S "D:\\deploy\\HCM\\logs"'
                bat 'if exist "D:\\deploy\\HCM\\*.config" DEL /Q "D:\\deploy\\HCM\\*.config"'
            }
        }
    }
}

----prueba master