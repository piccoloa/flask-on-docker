# https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx/


#docker commands

500  docker-compose exec web python manage.py create_db
  501  docker-compose exec db psql --username=hello_flask --dbname=hello_flask_dev
  502  docker volume inspect flask-on-docker_postgres_data
  503  docker-compose exec web python manage.py seed_db
  504  docker-compose exec db psql --username=hello_flask --dbname=hello_flask_dev

########dev-test#########dev-test#####dev-test####dev-test####
# to build and start dev-test database
docker-compose build --no-cache
docker-compose up 


# to verify dev database was created and other db commands
docker-compose exec web python manage.py create_db
docker-compose exec web python manage.py seed_db

docker-compose exec db psql --username=hello_flask --dbname=hello_flask_dev

# verify volume was crated
docker volume inspect flask-on-docker_postgres_data

########production#########production#####production####
# to build and start production database
docker-compose -f docker-compose.prod.yml down -v
docker-compose -f docker-compose.prod.yml up -d --build
docker-compose -f docker-compose.prod.yml exec web python manage.py create_db

# view production database logs
docker-compose -f docker-compose.prod.yml logs -f

# to verify prduction database was created
docker-compose exec db psql --username=hello_flask --dbname=hello_flask_prod



########################################################
# test postgres tables and users from pg prompt
hello_flask_dev=# \c shows connected db
\dt list tables
\l list databases
\q quit
