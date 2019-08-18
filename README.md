# PSMovieStore
Example of simple ASP.Net Core web-site and ASP.Net Core Rest API web service are based on docker containers.
Solution is built on Top of Azure and is using Azure Container Registry and Azure Web Apps for Containers.

How to up and run this example:
1. Clone or download curren repository.
2. Install Docker for desktop and switch it to use Linux containers. Ensure that Docker is running.
3. Open project solution in Visual Studio and build all projects.
4. Run solution on the local host end ensure that opened web-site is able to display page with following information:
	Pricing API says:
	- value 1
	- value 2
	- ID of docker container with web-service
5. Repeat building solution in Release mode.
6. Run in command console: [docker image]
   Inspect the outpup and ensure that it contains following images:
	- psregistrydm.azurecr.io/psmoviestore  latest
	- psregistrydm.azurecr.io/pspricingapi  latest
7. Open powershell CLI as Administrator and run the [deploy.ps1] script from [ARM Template] folder using following commands:
	- [Set-ExecutionPolicy RemoteSigned] 
	- Type A and press Enter
	- [& "<Absolute path to deploy.ps1>\deploy.ps1"]
	- Input Azure subscription ID and press Enter
	- Input Resourse Group name for all resourses [psmoviestore] and press Enter
	- Input name of deployment [InitialDeployment] and press Enter
	- Proceed with login authorization in Azure
	- In case of question about Resourse Group location, input required Azure Location [West Europe] and press Enter
	- Ensure that script completed without any errors
8. Login to Azure portal end ensure that following resourses were created:
	- Resource Group, which will contain next resourses:
	- - Container registry - psregistrydm
	- - App Service plan - psmoviestoredm
	- - App Service - psmoviestoredm
9. Open CMD and login to just created Azure Container registry using following command:
	- [az acr login --name psregistrydm]
10. Push docker images of the solution to ACR:
	- [docker push psregistrydm.azurecr.io/pspricingapi]
	- [docker push psregistrydm.azurecr.io/psmoviestore]
11. Inspect repositories in ACR:
	- psmoviestore and pspricingapi are created
12. Open Container Settings for Web App for Containers and switch Image source to Azure Container Registry.
	- In the Registry dropdown select psregistrydm
	- Click Choose File button and select docker-compose.yml file from the solution folder.
	- Click Save button in the buttom of the page.
13. From the psmoviestoredm App Service Overview blade copy URL value and open it in browser.
	- This step may take some time due to running containers in the Azure.
	- Finally you have to see the same web-site page as for local execution previously on step 4.
		
	
	
	
