### 4- Desarrollo:

#### 4.1 Modificar nuestro pipeline para incluir el deploy en QA y PROD de Imagenes Docker en Servicio Azure App Services con Soporte para Contenedores
- Desarrollo del punto 4.1: 
	
  	- ##### 4.1.1 - Agregar a nuestro pipeline una nueva etapa que dependa de nuestra etapa de Construcción y Pruebas y de la etapa de Construcción de Imagenes Docker y subida a ACR realizada en el TP08
  	    
  	  - Agregar tareas para crear un recurso Azure Container Instances que levante un contenedor con nuestra imagen de back utilizando un AppServicePlan en Linux
  	  ```yaml
		#---------------------------------------
		### STAGE DEPLOY TO AZURE APP SERVICE QA
		#---------------------------------------
		- stage: DeployImagesToAppServiceQA
		  displayName: 'Desplegar Imagenes en Azure App Service (QA)'
		  dependsOn: 
		  - BuildAndTestBackAndFront
		  - DockerBuildAndPush
		  condition: succeeded()
		  jobs:
		    - job: DeployImagesToAppServiceQA
		      displayName: 'Desplegar Imagenes de API y Front en Azure App Service (QA)'
		      pool:
		        vmImage: 'ubuntu-latest'
		      steps:
		        #------------------------------------------------------
		        # DEPLOY DOCKER API IMAGE TO AZURE APP SERVICE (QA)
		        #------------------------------------------------------
		        - task: AzureCLI@2
		          displayName: 'Verificar y crear el recurso Azure App Service para API (QA) si no existe'
		          inputs:
		            azureSubscription: '$(ConnectedServiceName)'
		            scriptType: 'bash'
		            scriptLocation: 'inlineScript'
		            inlineScript: |
		              # Verificar si el App Service para la API ya existe
		              if ! az webapp list --query "[?name=='$(WebAppApiNameContainersQA)' && resourceGroup=='$(ResourceGroupName)'] | length(@)" -o tsv | grep -q '^1$'; then
		                echo "El App Service para API QA no existe. Creando..."
		                # Crear el App Service sin especificar la imagen del contenedor
		                az webapp create --resource-group $(ResourceGroupName) --plan $(AppServicePlanLinux) --name $(WebAppApiNameContainersQA) --deployment-container-image-name "nginx"  # Especifica una imagen temporal para permitir la creación
		              else
		                echo "El App Service para API QA ya existe. Actualizando la imagen..."
		              fi
		
		              # Configurar el App Service para usar Azure Container Registry (ACR)
		              az webapp config container set --name $(WebAppApiNameContainersQA) --resource-group $(ResourceGroupName) \
		                --container-image-name $(acrLoginServer)/$(backImageName):$(backImageTag) \
		                --container-registry-url https://$(acrLoginServer) \
		                --container-registry-user $(acrName) \
		                --container-registry-password $(az acr credential show --name $(acrName) --query "passwords[0].value" -o tsv)
		              # Establecer variables de entorno
		              az webapp config appsettings set --name $(WebAppApiNameContainersQA) --resource-group $(ResourceGroupName) \
		                --settings ConnectionStrings__DefaultConnection="$(cnn-string-qa)" \
	
  	  ```

	![captura](imagenes/1.png)
	![captura](imagenes/2.png)
	![captura](imagenes/3.png)
	![captura](imagenes/4.png)
	![captura](imagenes/5.png)
   
#### 4.2 Desafíos:
- 4.2.1 Agregar tareas para generar Front en Azure App Service con Soporte para Contenedores

![captura](imagenes/6.png)
![captura](imagenes/7.png)
![captura](imagenes/8.png)
![captura](imagenes/9.png)
![captura](imagenes/10.png)

- 4.2.2 Agregar variables necesarias para el funcionamiento de la nueva etapa considerando que debe haber 2 entornos QA y PROD para Back y Front.

![captura](imagenes/11.png)
![captura](imagenes/12.png)

- 4.2.3 Agregar tareas para correr pruebas de integración en el entorno de QA de Back y Front creado en Azure App Services con Soporte para Contenedores. 

![captura](imagenes/13.png)
![captura](imagenes/14.png)

- 4.2.4 Agregar etapa que dependa de la etapa de Deploy en QA que genere un entorno de PROD.

![captura](imagenes/15.png)
![captura](imagenes/16.png)
![captura](imagenes/17.png)
![captura](imagenes/18.png)
![captura](imagenes/19.png)
![captura](imagenes/20.png)
![captura](imagenes/21.png)
![captura](imagenes/22.png)
![captura](imagenes/23.png)

- 4.2.5 Entregar un pipeline que incluya:

	El pipeline se encuentra en: https://dev.azure.com/TomiGarbe/Sample01/_build/results?buildId=355&view=results

	![captura](imagenes/24.png)

  - A) Etapa Construcción y Pruebas Unitarias y Code Coverage Back y Front

	![captura](imagenes/25.png)
	![captura](imagenes/26.png)
  
  - B) Construcción de Imágenes Docker y subida a ACR

	![captura](imagenes/27.png)

  - C) Deploy Back y Front en QA con pruebas de integración para Azure Web Apps

	![captura](imagenes/28.png)

  - D) Deploy Back y Front en QA con pruebas de integración para ACI

	![captura](imagenes/29.png)

  - E) Deploy Back y Front en QA con pruebas de integración para Azure Web Apps con Soporte para contenedores

	![captura](imagenes/30.png)

  - F) Aprobación manual de QA para los puntos C,D,E

	![captura](imagenes/31.png)
	![captura](imagenes/32.png)
	![captura](imagenes/33.png)
	![captura](imagenes/34.png)

  - G) Deploy Back y Front en PROD para Azure Web Apps

	![captura](imagenes/35.png)

  - H) Deploy Back y Front en PROD para ACI

	![captura](imagenes/36.png)

  - I) Deploy Back y Front en PROD para Azure Web Apps con Soporte para contenedores

	![captura](imagenes/37.png)
