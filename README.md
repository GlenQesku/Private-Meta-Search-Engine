# searxng-docker

Create a new SearXNG  instance in five minutes using Docker

# 🔍 Private Meta-Search Engine (SearXNG)

## 📌 Overview
This project is a self-hosted instance of **SearXNG**, a privacy-respecting, hackable meta-search engine. Deployed using Docker and Docker Compose on a Linux environment, it acts as a proxy between the user and external search engines (like Google, Bing, and DuckDuckGo). 

This architecture ensures that search queries are completely anonymized. SearXNG generates random search profiles for every query, stripping out tracking data and preventing external engines from building an advertising profile based on IP addresses or search history.

 ## 🌐 Live Demo

  You don't need to install anything to see it in action — a live instance is running here:

### 👉 **[glenqesku.duckdns.org](https://glenqesku.duckdns.org)**

  Search for anything and you'll get results aggregated from multiple engines
  (Google, Bing, DuckDuckGo, and more) — with **no ads, no trackers, and no
  saved search history**. Note the `https://` padlock: every request is proxied
  through the server, so the upstream search engines only ever see the *server's*
  IP, never yours. That's the whole privacy idea, working live.

  > ⚠️ This is a small personal instance on a free-tier server, provided as a demo —
  > it may be slow or occasionally offline. For real, reliable use, follow the
  > steps below to spin up **your own** instance in about five minutes.

## 🚀 Key Features
* **Total Anonymity:** Prevents data harvesting by proxying all requests through a single server IP.
* **Ad-Free Experience:** Automatically strips advertisements and tracking scripts from search results.
* **No Search History:** The server does not log queries or store user data.
* **Containerized Deployment:** Built entirely with Docker for easy replication, isolated environments, and rapid teardown/rebuilds.
* **Custom Configuration:** Modified `settings.yml` to optimize UI behavior (e.g., changing POST requests to GET for better browser navigation) and enable strict safe search.

## 🛠️ Technology Stack
* **Infrastructure:** Linux (Ubuntu), Docker, Docker Compose.
* **Application:** SearXNG (Meta-Search Engine).
* **Web Server / Reverse Proxy:** Caddy.
* **Database / Cache:** Redis.
* **Configuration:** YAML, Bash.

## 📁 Repository Structure
* `docker-compose.yml`: Defines the multi-container architecture (SearXNG, Redis, Caddy).
* `settings.yml`: The core configuration file dictating search engine behavior, UI preferences, and enabled search modules.
* `.env`: A template demonstrating the required environment variables (domain name, SSL email) without exposing live secrets.

## What is included ?

| Name | Description | Docker image | Dockerfile |
| -- | -- | -- | -- |
| [Caddy](https://github.com/caddyserver/caddy) | Reverse proxy (create a LetsEncrypt certificate automatically) | [caddy/caddy:2-alpine](https://hub.docker.com/_/caddy) | [Dockerfile](https://github.com/caddyserver/caddy-docker) |
| [SearXNG](https://github.com/searxng/searxng) | SearXNG by itself | [searxng/searxng:latest](https://hub.docker.com/r/searxng/searxng) | [Dockerfile](https://github.com/searxng/searxng/blob/master/Dockerfile) |
| [Redis](https://github.com/redis/redis) | In-memory database | [redis:alpine](https://hub.docker.com/_/redis) | [Dockerfile-alpine.template](https://github.com/docker-library/redis/blob/master/Dockerfile-alpine.template) |

## How to use it
- Install docker
- ```sh
  sudo apt install docker.io -y
  
- Install docker-compose
- ```sh
  sudo apt install docker-compose -y
   ```
    
- Get searxng-docker
  ```sh
  cd /usr/local
  git clone https://github.com/GlenQesku/Private-Search-Engine.git
  cd Private-Search-Engine/searxng-docker
  ```
- Edit the .env file to set the hostname and an email if you plan to run it online. 
- ```sh
  nano .env
- Generate the secret key
- ```sh
  sed -i "s|ultrasecretkey|$(openssl rand -hex 32)|g" searxng/settings.yml
  
- Edit the searxng/settings.yml file according to your need
- ```sh
  nano searxng/settings.yml
- Run SearXNG in the background:
- ```sh
  docker-compose up -d
- Finally enter the domain name that you put in the .env file, into your borwser. If you didnt change the .env file, run it localy into your browser http://localhost:8080/ .
  
