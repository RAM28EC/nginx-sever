# nginx-sever
lets talk about nginx sever
nginx server serve the web pages its feature is Load balancing , reverse proxy, redirecting the pages and caching .
here exmple as ubuntu 20.4
sudo apt install update -y
sudo apt install  nginx -y
cd /var/www/html
sudo vi index.html
:wq
cd /etc/nginx/sites-available
sudo vi default
server {
	listen 80;
	server_name localhost;
	location /{
	root /var/www/html;
        index index.html;
}
}
:wq
creating soft link 
sudo ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default
sudo nginx -t
sudo systemctl restart nginx
ifconfig
nginxpublicip
lets take another example
for dockerize and then we docker run on any port and expose to outside world (publicip:5000)this not good concept so for that we use here nginx reverse proxy
We know that locl host is http://127.0.0.1
so for that we will go to cd /etc/nginx/sites-enabled/
sudo vi default 
some changes
location /{
        proxy_pass http://127.0.0.1:5000;
}
location /backend {
        proxy_pass http://127.0.0.1:5000/backend;
}
sudo nginx -t
sudo systemctl nginx restart
ifconfig
publicip
thank you!!

