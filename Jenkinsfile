node {
  library('vapps')
  stage 'Init'
  checkout scm

  outputdir="${env.WORKSPACE}\\build"
  
  dotnet=dotnetFactory(tool('MSBuild15'), "packages\\xunit.runner.console.2.2.0\\tools\\xunit.console.exe")
	nuget=nugetFactory()
	build=buildFactory()
  
  // build pipeline
  build.pipeline {
	build.
		 stage('Build') {
			dotnet.msbuild('ManagedWinapi.sln',"Release", "\"/p:OutDir=${outputdir}\"")
		}
		state('Publish'){
			nuget.
				pack('ManagedWinapi/ManagedWinapi.csproj')
		}
  }

  // artifacts
  archiveArtifacts 'build/**'
}