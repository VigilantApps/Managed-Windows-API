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
			dotnet.
				msbuild('ManagedWinapi.sln',"Release")
		}
		stage('Publish'){
			nuget.
				pack(proj: 'ManagedWinapi/ManagedWinapi.csproj').
				publish(package: 'ManagedWinapi.0.3.0.nupkg')
		}
  }

}