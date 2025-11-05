- Frontend
  - npm install->it installs the dependencies.
  - npm run build
  - sudo apt update
  - sudo apt install ngnix
  - sudo systemctl start nginx(Nginx is a gatekeeper)
  - sudo systemctl enable nginx
  - Copy code from dist(build files) to /var/www/html/(sudo scp -r dist/\* /var/www/html/)
  - Enable port :80 of your instance.
- Backend

  - allowed ec2 insatance public IP on mongoDB server.
  - installed pm2(npm install pm2 -g)
  - pm2 start npm -- start
  - for giving custom name to your process(pm2 start npm --name "devtinder-backend" -- start)
  - pm2 logs
  - pm2 flush <name>,pm2 stop <name>,pm2 delete <name>
  - config nginx - sudo nano /etc/nginx/sites-available/default(for maping :3000 to /api where we can access our backend).
  - restart nginx- sudo systemctl restart nginx
  - modify the BASE_URL in frontend project to "/api"

# nginx configuration

    frontend=https://13.51.106.89/
    backend=https://13.51.106.89:3000/

    Domain name=devtinder.com=>13.51.106.89

    frontend=devtinder.com
    backend=devtinder.com:3000=>devtinder.com/api
