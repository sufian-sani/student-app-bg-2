Nginx setting:
/etc/nginx/conf.d  ==> 

upstream student_app {
    # This is the ACTIVE container
    server 127.0.0.1:5002;  # Change to 5002 when green is active
}

server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://student_app;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Connection "";
    }
}

