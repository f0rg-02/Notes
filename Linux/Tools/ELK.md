To install via docker: `sudo docker compose up -d elasticsearch filebeat kibana`

**NOTE: Does take a few minutes for everything to come up after running docker compose up**

- To enable security you apparently need to edit the `elasticsearch.yml`, but with docker this is done in the `docker-compose.yml`
- Not sure if this is correct

-------

But in the `elasticsearch.yml` to configure security:

```Ruby
xpack.security.enabled: true
xpack.security.authc.api_key.enabled: true
```

**NOTE: Looks like you have to set the password for user**

```yaml
elasticsearch:
    container_name: elasticsearch
    ...
    environment:
      ...
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - ELASTIC_PASSWORD=MyPassword # password for default user: elastic
	  ...
kibana:
	container_name: kibana
	...
	environment:
	...
	  - ELASTICSEARCH_USERNAME=elastic
      - ELASTICSEARCH_PASSWORD=MyPassword
	  - xpack.security.enabled=true # have to also have this for kibana
	...
...
```
------

To bring docker down: `sudo docker compose down -v`

To prune docker system images and anything else unused: `sudo docker system prune -a`
- Pressy 'Y' to confirm
- I've found doing this helps a lot after making some new changes to docker configuration files since there aren't any excess containers and images that could cause problems/errors to the previously built containers and images.