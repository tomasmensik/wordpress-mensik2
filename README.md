Automate your WordPress development workflow.
# INSTALL 
git clone https://github.com/petrgru/wordpress-docker

cd wordpress-docker

cp env.config .env

nano .env #change what is need password!!!!!!!!

docker-compose build

docker-compose up -d

sudo chmod 777 -R build/wordpress


# INSTALL WORDPRESS BY CLI
docker-compose run --rm wpcli wp core install --url=your_domain --title=Your_Blog_Title --admin_user=username --admin_password=password --admin_email=your_email.com

# BACKUP WORDPRESS DATABASE BY CLI
docker exec -it [db] mysqldump -u [user] -p[password] [database] > [file.sql]

#default config

docker exec -it wordpress-docker_db_1 mysqldump -u root -proot wordpress > zaloha.sql

# RESTORE DB WORDPRESS
cat zaloha.sql | docker exec -i wordpress-docker_db_1 mysql -u root -proot wordpress 


# BACKUP FILE SYSTEM
tar cvfz wordpress.tar.gz build/wordpress

# RESTORE FILE SYSTEM
sudo tar xvfz wordpress.tar.gz -C ./

sudo chmod 777 -R build/wordpress

# CHANGE URL inside WP instance
docker-compose run --rm wpcli wp search-replace [OLD_URL] [NEW_URL] --all-tables
