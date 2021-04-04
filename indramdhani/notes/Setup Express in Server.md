1.  go to the nodejs specific directory and create new directory
    
    ```bash
    # it is not always same in all server
    cd /media/site_data/nodejs
    mkdir project_node
    ```
    
2.  Clone the project and install dependencies
    
    ```bash
    cd project_node
    git clone url-project .
    npm install
    ```
    
3.  Create ecosystem for the project\_node
    
    ```bash
    cd /media/site_data/nodejs
    nano ecosystem.config.js
    ```
    
    add the block below (adjust the value of the parameter)
    
    ```bash
    {
      name: 'project-name',
      script: 'index.js',
      cwd: '/media/site_data/nodejs/project_node',
      // Options reference: <https://pm2.io/doc/en/runtime/reference/ecosystem-file/>
      instances: 'max',
      autorestart: true,
      watch: [
        'config',
        'routes',
        'services',
        'subscribers',
      ],
      ignore_watch: ['node_modules', '.git'],
      max_memory_restart: '256M',
      time: true,
      env: {
        NODE_ENV: 'testing',
      },
      env_production: {
        NODE_ENV: 'testing',
      },
    },
    ```
    
4.  Start the service
    
    ```bash
    cd /media/site_data/nodejs
    pm2 start ecosystem.config.js --only project-name
    ```
    
5.  Create virtual host configuration
    
    ```bash
    cd /etc/httpd/conf.vhost.d
    ```
    
    Option 1
    
    ```bash
    ProxyPass "/path/to/open/the/service/" <http://127.0.0.1>:portnumber/
    ProxyPassReverse "/path/to/open/the/service/" <http://127.0.0.1>:portnumber/
    ```
    
    Option 2
    
    ```bash
    <VirtualHost *:80>
        ProxyPreserveHost On
        ProxyPass / <http://127.0.0.1>:portnumber/
        ProxyPassReverse / <http://127.0.0.1>:portnumber/
        ServerName url.to.open.the.service
    </VirtualHost>
    ```
    
6.  Add subdomain into the dns
    
    -   login to the dns provider
    -   add new a record and set the target to the server ip address
7.  Setup the https configuration
    
    Add https configuration to the httpd config. Use certbot if it is possible.
    
8.  check the httpd config
    
    ```bash
    sudo httpd -t
    ```
    
9.  reload the service
    
    ```bash
    sudo service httpd reload
    ```
    
10.  update the pm2 startup code
    
    ```bash
    pm2 unstartup
    pm2 startup
    ```
	
#server #express #pm2