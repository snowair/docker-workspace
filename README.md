# My PHP development docker workspace

Start a full php development(nginx+php+mysql+redis+memcache+mongodb+elasticsearch) workspace by run : `docker-compose up`.

```
.
├── compose
│   ├── nginx+fpm
│   │   ├── common.yml                  # base dockerr compose config, used for extend
│   │   └── docker-compose.yml.example  # a config example, copy and edit it as your compose config file.
│   ├── elk
│   │   └── docker-compose.yml
│   └── rocket.chat
│       ├── docker-compose.yml
│       └── uploads
├── data                                # data persistent directory
│   ├── elasticsearch
│   └── redis
├── Dockerfiles
│   ├── debian-php-base
│   │   ├── Dockerfile                  # Used to build a OS image suite for PHP devlepment
│   │   ├── sources.list                # default apt sources
│   │   └── 163-sources.list            # apt sources for people in China
│   ├── elk
│   │   ├── elasticsearch
│   │   │   └── Dockerfile
│   │   └── kibana
│   │       └── Dockerfile
│   └── oracle
│       └── Dockerfile
├── env
├── etc
│   ├── mysql                          # mysql configuration
│   │   ├── conf.d                    
│   │   │   ├── max_allowed_packet.cnf
│   │   │   ├── sql_mode.cnf
│   │   │   └── time_zone.cnf
│   │   └── my.cnf
│   ├── nginx
│   │   ├── conf.d                     # nginx configuration examples for some PHP Frameworks
│   │   │   ├── default.conf
│   │   │   ├── ci.conf.example
│   │   │   ├── laravel.conf.example
│   │   │   ├── pahlcon.conf.example
│   │   │   ├── slim.conf.example
│   │   │   ├── symfony.conf.example
│   │   │   ├── thinkphp.conf.example
│   │   │   ├── yii2.conf.example
│   │   │   └── zf.conf.example
│   │   ├── fastcgi_params
│   │   ├── koi-utf
│   │   ├── koi-win
│   │   ├── mime.types
│   │   ├── nginx.conf
│   │   ├── scgi_params
│   │   ├── server.crt
│   │   ├── server.csr
│   │   ├── server.key
│   │   ├── server.key.org
│   │   ├── uwsgi_params
│   │   └── win-utf
│   └── php
│       ├── conf.d                       # php ext config files, you can use them to replace the same name ini files in the php contianer by Data valumes.
│       │   ├── docker-php-ext-apc.ini
│       │   ├── ...
│       │   └── docker-php-ext-zip.ini
│       ├── php-fpm.conf                 # real effective fpm config.
│       ├── php-fpm.conf.default
│       ├── php.ini-development          # real effective php config.
│       ├── php.ini-production
│       └── zend_extensions
│           ├── opcache-setting.ini      # real effective opcache config.
│           └── xdebug-setting.ini       # real effective xdebug config.
└── README.md
```

# Persistent oracle db data

follow these steps:

1. open `compose/nginx+fpm/compose.yml`, modify oracle volumes config to :
    ```
    # - /opt/u01:/u01
    - /opt/u01:/opt/u01
    ```

2. start compose containers

3. enter in the runing oracle container, run :
    ```
    # service oracle-xe stop
    # mv /u01/* /opt/u01
    # exit
    ```

4. stop compose contianers

5. open `compose/nginx+fpm/compose.yml`, modify oracle volumes config to :
    ```
    - /opt/u01:/u01
    # - /opt/u01:/opt/u01
    ```

6. start compose containers
