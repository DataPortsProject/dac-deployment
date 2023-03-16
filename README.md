# Data Access Component deployment

This repository contains the docker-compose file necessary to deploy the required components to make the DAC work: Orion, Cygnus, API, Web Client and  databases.


You will need to clone at least the following repos (do not remane default directory names in the working copy):
- https://egitlab.iti.es/dataports/data_access/data-access-manager-api
- https://egitlab.iti.es/dataports/data_access/data-access-manager-ui
- https://egitlab.iti.es/dataports/data_access/mongo-seed-datamodels
- https://egitlab.iti.es/dataports/data_access/mongo-seed-templates



Your DAC folder should look like (once repos are cloned) this:
- data-access-deployment
- data-access-manager-api
- data-access-manager-ui
- mongo-seed-templates
- mongo-seed-datamodels


To run the stack, simply issue the command:

```docker-compose -p <your _stack_name> up -d --build```


# Setup services
By default, the ```docker-compose``` contains the basic setup to run the whole component without without a proxy (all entpoints and ports should be reachable locally).
If you plan to add a proxy, you may need to adjust endpoints in ```data-access-manager-ui/src\utils\constants.js``` by changing the values of ```baseURL_DAM_API``` and ```baseURL_API_ON_DEMAND```


The configuration params exposed in the docker-compose file are set in the ```dataports-api``` service. These are:

| Name         | Description                                                                                                                                                                                      |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ENABLE_CORS  | If enabled, the API will add CORS headers to all requests. Defaults to ```true```                                                                                                                |
| NODE_ENV     | Controls the source code compilation mode. Defaults to ```production```                                                                                                                          |
| INSECURE_WS  | If set to true, websocket communications will use the unsecure protocol. This setups is just for debugging or if you plan to proxy the websocket. Defaults to ```false```                        |
| MONGO_URL    | URL of the mongo instance used by teh API. Defaults to ```mongodb://mongo/dataports-db```                                                                                                        |
| DOCKER_API   | IP address of the internal docker engine's REST API. Note that you may need to enable it as described in https://docs.docker.com/engine/api/. Defaults to ```http://host.docker.internal:2375``` |
| ORION_URL    | IP address of Orion Context Broker. Defaults to ```http://orion:1026```                                                                                                                          |
| CYGNUS_URL   | IP address of Cygnus. Defaults to ```http://cygnus:5055```                                                                                                                                       |
| NODERED_URL  | IP address of ICCS component. Defaults to  ```http://node-red:1880```                                                                                                                            |
| KEYCLOAK_URL | IP address of the Keycloak instace used for authentication. Defaults to ```https://iam.dataports.com.es:8443```                                                                                  |