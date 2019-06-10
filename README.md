# RestJersyAngularJs

***Coté server:***

dans server.js: 

```
public Response returnRespCORS(Object obj) {
		return Response.status(200)
				.header("Access-Control-Allow-Origin", "*")
			      .header("Access-Control-Allow-Credentials", "true")
			      .header("Access-Control-Allow-Headers",
			        "origin, content-type, accept, authorization")
			      .header("Access-Control-Allow-Methods", 
			        "GET, POST, PUT, DELETE, OPTIONS, HEAD")
			      .entity(obj).build();
	}
```

```
	@GET
	@Path("/{name}")
	public Response getMsgPath( @PathParam("name") String msg) {
 		ModelTest res = new ModelTest(1, msg);
		return returnRespCORS(res);
	}
	
	@POST
	@Path("posttest")
	@Consumes(MediaType.APPLICATION_JSON)
	@Produces(MediaType.APPLICATION_JSON)
	public ModelTest tstJson(ModelTest obj) throws IOException {
		obj.setName("NewName HHH");
		return obj;
	}
```

web.xml
```
<servlet>
		<servlet-name>jersey-serlvet</servlet-name>
		<servlet-class>com.sun.jersey.spi.container.servlet.ServletContainer</servlet-class>
		<init-param>
			<param-name>com.sun.jersey.config.property.packages</param-name>
			<param-value><myPackageNameWithRestClasses></param-value>
		</init-param>
		<init-param>
			<param-name>com.sun.jersey.api.json.POJOMappingFeature</param-name>
			<param-value>true</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>

	<servlet-mapping>
		<servlet-name>jersey-serlvet</servlet-name>
		<url-pattern>/rest/*</url-pattern>
	</servlet-mapping>
  ```
  
  pom.xml
  ```
  <dependency>
			<groupId>com.sun.jersey</groupId>
			<artifactId>jersey-server</artifactId>
			<version>1.8</version>
		</dependency>

		<dependency>
			<groupId>com.sun.jersey</groupId>
			<artifactId>jersey-json</artifactId>
			<version>1.8</version>
		</dependency>
  ```
  
  ***Coté Client:***
  
  ```
    
  $http({
          method : "GET",
            url : "http://localhost:8080/RESTfulExample/rest/hello/moummid"
            }).then(function mySuccess(response) {
                $scope.lastName = response.data.name;
            }, function myError(response) {
                $scope.lastName = response.statusText;
            });
            
   ```
  
