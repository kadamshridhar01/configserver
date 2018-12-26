# configserver
Spring Config server .Create the server where we can read the properties from git .depend on Env.

#Enable COnfig server
@SpringBootApplication
@EnableConfigServer
public class ConfigserverApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConfigserverApplication.class, args);
	}
}

#application properties changes
server.port=8888
#project run port number
spring.cloud.config.server.git.uri=https://github.com/kadamshridhar01/springConfig-dev.git
#Git location where the property files stored.
management.security.enabled=false
#Enable endpoint like Env make testing easy for us.


#calling property from differnt Env .please refer git project springconfig-dev project repository.
Get request like http://localhost:${server.port}/${spring.application.name}/${Env}
curl -get http://localhost:8888/orderservice/prod 
response :- you will get the all properties as key value.
{
    "name": "orderservice",
    "profiles": [
        "prod"
    ],
    "label": null,
    "version": "c8d1d2d1624749392a145c38427d075aff495d6a",
    "state": null,
    "propertySources": [
        {
            "name": "https://github.com/kadamshridhar01/springConfig-dev.git/orderservice-prod.properties",
            "source": {
                "spring.rabbitmq.host": "localhost.prod",
                "spring.rabbitmq.port": "5672.prod",
                "spring.rabbitmq.username": "guest.prod",
                "spring.rabbitmq.password": "guest.prod"
            }
        },
        {
            "name": "https://github.com/kadamshridhar01/springConfig-dev.git/orderservice.properties",
            "source": {
                "spring.rabbitmq.host": "localhost",
                "spring.rabbitmq.port": "5672",
                "spring.rabbitmq.username": "guest",
                "spring.rabbitmq.password": "guest"
            }
        }
    ]
}
