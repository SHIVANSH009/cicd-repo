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
				sh 'sudo mkdir -p /code/isis/latest'
				sh 'sudo cp /var/lib/jenkins/workspace/isis/target/addressbook.war /code/isis/latest/'
				sh 'sudo cp /var/lib/jenkins/workspace/isis/Dockerfile /code/isis/latest/'
				sh 'sudo docker build -f /code/isis/latest/Dockerfile -t palakagrawal25/ab-30jan2022:latest /code/isis/latest'
			}
		}

		stage('Push Docker Image')
		{
			steps
			{
				sh 'sudo docker push palakagrawal25/ab-30jan2022:latest'
			}
		}

		stage('Update Application')
		{
			steps
			{
				sh 'sudo docker run -itd -P palakagrawal25/ab-30jan2022:latest'
			}
		}
		
	}
		
}
