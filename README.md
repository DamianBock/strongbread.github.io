# strongbread.github.io

First color pallete choice
--text: #424148;
--background: #fffceb;
--primary: #fdcc72;
--secondary: #632808;
--accent: #4a4c92;


Second color pallete choice
--text: #424148;
--background: #fffceb;
--primary: #624520;
--secondary: #eed4cc;
--accent: #b5dfa7;


## SSL Certificate Setup with Docker Compose

Follow these steps to generate your SSL certificates using a temporary bootstrap configuration before switching to your production environment.

### Step 1: Start the Bootstrap Environment
Initialize the temporary container setup required to perform the ACME challenge.

```bash
docker-compose -f docker-compose.init.yml up -d
```

### Step 2: Generate the Certificates
Run the ephemeral Certbot container to request certificates for your specific domains.

```bash
docker-compose -f docker-compose.init.yml run --rm certbot certonly --webroot --webroot-path /var/www/certbot -d strongbread.com -d [www.strongbread.com](https://www.strongbread.com)
```

### Step 3: Switch to Production
Once the certificates are successfully generated, tear down the bootstrap environment and spin up the actual production containers.

**1. Stop the bootstrap containers:**
```bash
docker-compose -f docker-compose.init.yml down
```

**2. Start the production containers:**
```bash
docker-compose up -d
```