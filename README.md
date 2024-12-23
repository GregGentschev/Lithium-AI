<div align="center">
<img src="https://x.com/Lithium_AI/photo" width="520" alt="Lithium AI">
</a>
</div>

<p align="center">
    <a href="https://x.com/intent/follow?screen_name=Lithium_AI" target="_blank">
        <img src="https://img.shields.io/twitter/follow/Lithium_AI?logo=X&color=%20%23f5f5f5" alt="follow on X(Twitter)">

    <a href="https://hub.docker.com/r/Lithium-AI/Lithium_AI" target="_blank">
        <img src="https://img.shields.io/badge/docker_pull-Lithium_AI:v0.15.0-brightgreen" alt="docker pull GregGentschev/Lithium-AI:v0.15.0">
    </a>
    <a href="https://github.com/GregGentschev/Lithium-AI/blob/main/LICENSE">
        <img height="21" src="https://img.shields.io/badge/License-Apache--2.0-ffffff?labelColor=d4eaf7&color=2e6cc4" alt="license">
    </a>
</p>

<details open>
<summary></b>📕 Table of Contents</b></summary>

- 💡 [What is Lithium-AI?](#-what-is-Lithium-AI)
- 📌 [Latest Updates](#-latest-updates)
- 🌟 [Key Features](#-key-features)
- 🔎 [System Architecture](#-system-architecture)
- 🎬 [Get Started](#-get-started)
- 🔧 [Configurations](#-configurations)
- 🔧 [Build a docker image without embedding models](#-build-a-docker-image-without-embedding-models)
- 🔧 [Build a docker image including embedding models](#-build-a-docker-image-including-embedding-models)
- 🔨 [Launch service from source for development](#-launch-service-from-source-for-development)

</details>

## 💡 What is Lithium-AI?

Lithium-AI is an open-source RAG (Retrieval-Augmented Generation) engine based on deep document
understanding. It offers a streamlined RAG workflow for businesses of any scale, combining LLM (Large Language Models)
to provide truthful question-answering capabilities, backed by well-founded citations from various complex formatted
data.

## 🔥 Latest Updates

- 2024-12-18 Upgrades Document Layout Analysis model in Deepdoc.
- 2024-12-04 Adds support for pagerank score in knowledge base.
- 2024-11-22 Adds more variables to Agent.
- 2024-11-01 Adds keyword extraction and related question generation to the parsed chunks to improve the accuracy of retrieval.
- 2024-08-22 Support text to SQL statements through RAG.
- 2024-08-02 Supports GraphRAG inspired by [graphrag](https://github.com/microsoft/graphrag) and mind map.

## 🌟 Key Features

### 🍭 **"Quality in, quality out"**

- Deep document understanding based knowledge extraction from unstructured data with complicated
  formats.
- Finds "needle in a data haystack" of literally unlimited tokens.

### 🍱 **Template-based chunking**

- Intelligent and explainable.
- Plenty of template options to choose from.

### 🌱 **Grounded citations with reduced hallucinations**

- Visualization of text chunking to allow human intervention.
- Quick view of the key references and traceable citations to support grounded answers.

### 🍔 **Compatibility with heterogeneous data sources**

- Supports Word, slides, excel, txt, images, scanned copies, structured data, web pages, and more.

### 🛀 **Automated and effortless RAG workflow**

- Streamlined RAG orchestration catered to both personal and large businesses.
- Configurable LLMs as well as embedding models.
- Multiple recall paired with fused re-ranking.
- Intuitive APIs for seamless integration with business.

## 🔎 System Architecture

<div align="center" style="margin-top:20px;margin-bottom:20px;">
<img src="https://github.com/infiniflow/ragflow/assets/12318111/d6ac5664-c237-4200-a7c2-a4a00691b485" width="1000"/>
</div>

## 🎬 Get Started

### 📝 Prerequisites

- CPU >= 4 cores
- RAM >= 16 GB
- Disk >= 50 GB
- Docker >= 24.0.0 & Docker Compose >= v2.26.1
  > If you have not installed Docker on your local machine (Windows, Mac, or Linux),
  see [Install Docker Engine](https://docs.docker.com/engine/install/).

### 🚀 Start up the server

1. Ensure `vm.max_map_count` >= 262144:

   > To check the value of `vm.max_map_count`:
   >
   > ```bash
   > $ sysctl vm.max_map_count
   > ```
   >
   > Reset `vm.max_map_count` to a value at least 262144 if it is not.
   >
   > ```bash
   > # In this case, we set it to 262144:
   > $ sudo sysctl -w vm.max_map_count=262144
   > ```
   >
   > This change will be reset after a system reboot. To ensure your change remains permanent, add or update the
   `vm.max_map_count` value in **/etc/sysctl.conf** accordingly:
   >
   > ```bash
   > vm.max_map_count=262144
   > ```

2. Clone the repo:

   ```bash
   $ git clone https://github.com/GregGentschev/Lithium-AI
   ```

3. Start up the server using the pre-built Docker images:

   > The command below downloads the `v0.15.0-slim` edition of the Lithium-AI Docker image. Refer to the following table for descriptions of different Lithium-AI editions. To download an Lithium-AI edition different from `v0.15.0-slim`, update the `Lithium-AI` variable accordingly in **docker/.env** before using `docker compose` to start the server. For example: set `Lithium-AI=GregGentschev/Lithium-AI:v0.15.0` for the full edition `v0.15.0`.

   ```bash
   $ cd Lithium-AI
   $ docker compose -f docker/docker-compose.yml up -d
   ```

   | Lithium-AI image tag | Image size (GB) | Has embedding models? | Stable?                  |
   | ----------------- | --------------- | --------------------- | ------------------------ |
   | v0.15.0           | &approx;9       | :heavy_check_mark:    | Stable release           |
   | v0.15.0-slim      | &approx;2       | ❌                    | Stable release           |
   | nightly           | &approx;9       | :heavy_check_mark:    | *Unstable* nightly build |
   | nightly-slim      | &approx;2       | ❌                    | *Unstable* nightly build |

4. Check the server status after having the server up and running:

   ```bash
   $ docker logs -f Lithium-AI-server
   ```

   _The following output confirms a successful launch of the system:_

   ```bash

    * Running on all addresses (0.0.0.0)
    * Running on http://127.0.0.1:9380
    * Running on http://x.x.x.x:9380
    INFO:werkzeug:Press CTRL+C to quit
   ```
   > If you skip this confirmation step and directly log in to Lithium-AI, your browser may prompt a `network anormal`
   error because, at that moment, your Lithium-AI may not be fully initialized.

5. In your web browser, enter the IP address of your server and log in to Lithium-AI.
   > With the default settings, you only need to enter `http://IP_OF_YOUR_MACHINE` (**sans** port number) as the default
   HTTP serving port `80` can be omitted when using the default configurations.
6. In [service_conf.yaml.template](./docker/service_conf.yaml.template), select the desired LLM factory in `user_default_llm` and update
   the `API_KEY` field with the corresponding API key.

   _The show is on!_

## 🔧 Configurations

When it comes to system configurations, you will need to manage the following files:

- [.env](./docker/.env): Keeps the fundamental setups for the system, such as `SVR_HTTP_PORT`, `MYSQL_PASSWORD`, and
  `MINIO_PASSWORD`.
- [service_conf.yaml.template](./docker/service_conf.yaml.template): Configures the back-end services. The environment variables in this file will be automatically populated when the Docker container starts. Any environment variables set within the Docker container will be available for use, allowing you to customize service behavior based on the deployment environment.
- [docker-compose.yml](./docker/docker-compose.yml): The system relies on [docker-compose.yml](./docker/docker-compose.yml) to start up.

> The [./docker/README](./docker/README.md) file provides a detailed description of the environment settings and service
> configurations which can be used as `${ENV_VARS}` in the [service_conf.yaml.template](./docker/service_conf.yaml.template) file.

To update the default HTTP serving port (80), go to [docker-compose.yml](./docker/docker-compose.yml) and change `80:80`
to `<YOUR_SERVING_PORT>:80`.

Updates to the above configurations require a reboot of all containers to take effect:

> ```bash
> $ docker compose -f docker/docker-compose.yml up -d
> ```

### Switch doc engine from Elasticsearch to Infinity

Lithium-AI uses Elasticsearch by default for storing full text and vectors. To switch to [Infinity](https://github.com/Lithium-AI/infinity/), follow these steps:

1. Stop all running containers:

   ```bash
   $ docker compose -f docker/docker-compose.yml down -v
   ```

2. Set `DOC_ENGINE` in **docker/.env** to `infinity`.

3. Start the containers:

   ```bash
   $ docker compose -f docker/docker-compose.yml up -d
   ```

> [!WARNING] 
> Switching to Infinity on a Linux/arm64 machine is not yet officially supported.

## 🔧 Build a Docker image without embedding models

This image is approximately 2 GB in size and relies on external LLM and embedding services.

```bash
git clone https://github.com/GregGentschev/Lithium-AI.git
cd Lithium-AI/
docker build --build-arg LIGHTEN=1 -f Dockerfile -t GregGentschev/Lithium-AI:nightly-slim .
```

## 🔧 Build a Docker image including embedding models

This image is approximately 9 GB in size. As it includes embedding models, it relies on external LLM services only.

```bash
git clone https://github.com/GregGentschev/Lithium-AI.git
cd Lithium-AI/
docker build -f Dockerfile -t Lithium-AI:nightly .
```

## 🔨 Launch service from source for development

1. Install Poetry, or skip this step if it is already installed:
   ```bash
   pipx install poetry
   export POETRY_VIRTUALENVS_CREATE=true POETRY_VIRTUALENVS_IN_PROJECT=true
   ```

2. Clone the source code and install Python dependencies:
   ```bash
   git clone https://github.com/GregGentschev/Lithium-AI.git
   cd Lithium-AI/
   ~/.local/bin/poetry install --sync --no-root --with=full # install Lithium-AI dependent python modules
   ```

3. Launch the dependent services (MinIO, Elasticsearch, Redis, and MySQL) using Docker Compose:
   ```bash
   docker compose -f docker/docker-compose-base.yml up -d
   ```

   Add the following line to `/etc/hosts` to resolve all hosts specified in **docker/.env** to `127.0.0.1`:
   ```
   127.0.0.1       es01 infinity mysql minio redis
   ```  

4. If you cannot access HuggingFace, set the `HF_ENDPOINT` environment variable to use a mirror site:

   ```bash
   export HF_ENDPOINT=https://hf-mirror.com
   ```

5. Launch backend service:
   ```bash
   source .venv/bin/activate
   export PYTHONPATH=$(pwd)
   bash docker/launch_backend_service.sh
   ```

6. Install frontend dependencies:
   ```bash
   cd web
   npm install --force
   ```  
7. Launch frontend service:
   ```bash
   npm run dev 
   ```  

   _The following output confirms a successful launch of the system:_

   ![](https://github.com/user-attachments/assets/0daf462c-a24d-4496-a66f-92533534e187)

