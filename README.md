# kong-blog-tutorial
Setup to follow the blog entry

To up this setup for the first time:

```bash
docker-compose up -d
```

Once this has run and pulled all the required files, run docker ps

```bash
docker-compose ps

              Name                             Command               State                         Ports                      
------------------------------------------------------------------------------------------------------------------------------
kongblogtutorial_httpbin_1          gunicorn httpbin:app -b 0. ...   Up                                                       
kongblogtutorial_kong-database_1    /docker-entrypoint.sh cass ...   Up       7000/tcp, 7001/tcp, 7199/tcp, 9042/tcp, 9160/tcp
kongblogtutorial_kong-migration_1   /docker-entrypoint.sh /wai ...   Up       8000/tcp, 8001/tcp, 8443/tcp, 8444/tcp          
kongblogtutorial_kong_1             /docker-entrypoint.sh /usr ...   Exit 1 
```
> You should notice that the kong container has exited along with the kong  still running
this is because before kong will start the migration container has to run the migrations before kong container will run

when both containers show exited:

```bash
docker-compose ps

              Name                             Command               State                         Ports                      
------------------------------------------------------------------------------------------------------------------------------
kongblogtutorial_httpbin_1          gunicorn httpbin:app -b 0. ...   Up                                                       
kongblogtutorial_kong-database_1    /docker-entrypoint.sh cass ...   Up       7000/tcp, 7001/tcp, 7199/tcp, 9042/tcp, 9160/tcp
kongblogtutorial_kong-migration_1   /docker-entrypoint.sh /wai ...   Exit 0                                                   
kongblogtutorial_kong_1             /docker-entrypoint.sh /usr ...   Exit 1  
```

start the containers again:

```bash
docker-compose up -d
``` 
Your kong instance should be running now with the migration container still exited

```bash
docker-compose ps
              Name                             Command               State                                  Ports                               
------------------------------------------------------------------------------------------------------------------------------------------------
kongblogtutorial_httpbin_1          gunicorn httpbin:app -b 0. ...   Up                                                                         
kongblogtutorial_kong-database_1    /docker-entrypoint.sh cass ...   Up       7000/tcp, 7001/tcp, 7199/tcp, 9042/tcp, 9160/tcp                  
kongblogtutorial_kong-migration_1   /docker-entrypoint.sh /wai ...   Exit 0                                                                     
kongblogtutorial_kong_1             /docker-entrypoint.sh /usr ...   Up       0.0.0.0:8000->8000/tcp, 0.0.0.0:8001->8001/tcp, 8443/tcp, 8444/tcp
```

You are now ready to start the tutorial