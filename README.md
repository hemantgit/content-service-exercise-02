# Backbase Training Exercises

## Portal Backend - Module 2: Custom CS Validator

This example provides a Content Services validator that allows to upload only files of `bb:image` document type with *.png*, *.jpg* or *.jpeg* extensions.

### Installation & Configuration

- Clone this project into the **services** folder of your project

- Include content-service-exercise-02 module to the build. Open `services/pom.xml` and add **content-service-exercise-02** in the `<modules>` section:
	```xml
	    <modules>
	        ...	    
	        <module>content-service-exercise-02</module>
	        ...
	    </modules>
	```	
	Re-compile **services** by executing `mvn clean install` in the **services** folder.

- Add the newly created module in the Content Services application. In the `<dependencies>` section of `webapps/contentservices/pom.xml`, add the following dependency:

	```xml
	    <dependency>
	        <groupId>com.backbase.training</groupId>
	        <artifactId>content-service-exercise-02</artifactId>
	        <version>1.0-SNAPSHOT</version>
	    </dependency>
	```

	Copy `web.xml` file from `webapps/contentservices/target/contentservices/WEB-INF/web.xml` into `webapps/contentservices/src/main/webapp/WEB-INF` directory and change the following section:
	
	```xml
        <context-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>
                classpath:/META-INF/spring/bb-contentservices.xml
                classpath:/META-INF/spring/bb-validators.xml
                classpath:/META-INF/spring/backbase-contentservices-administration-business.xml
                classpath:/META-INF/spring/backbase-content-eventing-config.xml
                classpath:/META-INF/spring/backbase-content-search-config.xml
            </param-value>
        </context-param>
	```

	If you are already running content services, stop your jetty server. Otherwise, just proceed with the next step.     

- Register new validator in Content Services properties. Edit `configuration/src/main/resources/backbase.properties` file by adding the following property: 
    
    ```    
    # Validators (comma separated, order is important)
	contentservices.validators=com.backbase.portal.contentservices.validator.impl.RepositorySchemaValidator,com.backbase.portal.contentservices.validator.impl.CustomValidator
    ```
    Re-compile configuration module by running `mvn clean package` command from the **configuration** module.    

### Run & Test

- If Content Services application is already running, stop it by pressing *Ctrl+C*. Start Content Services application by executing `mvn jetty:run` command from the **webapps/contentservices** directory.
- Try to upload any `.gif` file to Content Services by using CMIS client and specifying the `bb:image` document type.
- Make sure the upload fails because of validation.
	
	
	
	
