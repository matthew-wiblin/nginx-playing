location / {
            proxy_pass http://your_upstream_server;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_intercept_errors on;
            error_page 500 502 503 504 = @retry;
            add_header X-Proxy "NGINX";
                proxy_next_upstream_timeout 3;
            proxy_next_upstream_tries 3;

        location = @retry {
            proxy_pass http://your_upstream_server;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            add_header X-Proxy "NGINX";
            }
        }