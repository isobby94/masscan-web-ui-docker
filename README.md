# masscan-web-ui-docker
MASSCAN Web UI with LEMP stack on Docker

## Requirements
- Docker
- Docker Compose

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/isobby94/masscan-web-ui-docker.git
cd masscan-web-ui-docker
```

### 2. Configure environment

Edit `docker-compose.yml` and change the default credentials:

```yaml
MARIADB_ROOT_PASSWORD: toor
MARIADB_PASSWORD: changem3
```

### 3. Start the containers

```bash
docker-compose up -d
```

### 4. Run masscan and save report

```bash
cd app
echo '192.168.0.0/16' > iplist.txt
docker exec -i masscan-web sh -c 'masscan -iL iplist.txt -oX report.xml --open --banners --rate 10000 -p1-65535'
```

### 5. Import report

```bash
docker exec -i masscan-php sh -c 'php import.php report.xml'
```

### 6. Open in browser
http://localhost


## Services

| Container | Description |
|-----------|-------------|
| `masscan-web` | Nginx web server |
| `masscan-php` | PHP-FPM |
| `masscan-db` | MariaDB 10.5 |

## License
GPL-2.0