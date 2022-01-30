pipeline
{
	agent any
	stages
	{
		stage('Checkout')
		{
			steps
			{
				git 'https://github.com/iamdevopstrainer/DevOpsClassCodes'
			}
		}
		
		stage('Compile')
		{
			steps
			{
				sh 'mvn compile'
			}
		}

		stage('Test')
		{
			steps
			{
				sh 'mvn test'
			}
		}

		stage('Build')
		{
			steps
			{
				sh 'mvn package'
			}
		}
		
		stage('Build Docker Image')
		{
			steps
			{
				sh 'sudo mkdir -p /code/isis/$BUILD_NUMBER'
				sh 'sudo cp /var/lib/jenkins/workspace/isis/target/website.war /code/isis/$BUILD_NUMBER/'
				sh 'sudo cp /var/lib/jenkins/workspace/isis/Dockerfile /code/isis/$BUILD_NUMBER/'
				sh 'sudo docker build -f /code/isis$BUILD_NUMBER/Dockerfile -t palakagrawaljk/ab-30jan2022:$BUILD_NUMBER /code/isis/$BUILD_NUMBER'
			}
		}

		stage('Push Docker Image')
		{
			steps
			{
				sh 'sudo docker push palakagrawaljk/ab-30jan2022:$BUILD_NUMBER'
			}
		}

		stage('Update Application')
		{
			steps
			{
				sh 'sudo docker run -itd -P palakagrawaljk/ab-30jan2021:$BUILD_NUMBER'
			}
		}
		
	}
		
}
