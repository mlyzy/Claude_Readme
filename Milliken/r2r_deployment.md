# R2R Deployment Documentation

## Overview
R2R is an advanced AI retrieval system that supports Retrieval-Augmented Generation (RAG) with a RESTful API. This document outlines the deployment process and requirements.

## System Requirements
- Python 3.x
- pip package manager
- OpenAI API key

## Installation Steps

### 1. Basic Installation (Light Mode)
```bash
# Install the R2R package
pip install r2r

# Set up OpenAI API key
export OPENAI_API_KEY=your_openai_api_key

# Run the service
python -m r2r.serve
```

### 2. Full Installation (Docker Mode)
```bash
# Clone the repository
git clone git@github.com:SciPhi-AI/R2R.git
cd R2R

# Set required environment variables
export R2R_CONFIG_NAME=full
export OPENAI_API_KEY=your_openai_api_key

# Start the services using Docker Compose
docker compose -f compose.full.yaml --profile postgres up -d
```

## Features
- Multimodal content ingestion
- Hybrid search capabilities
- Knowledge graph support
- RESTful API interface
- User and access management

## API Usage
After deployment, the API will be available at `http://localhost:7272`. You can interact with it using either Python or JavaScript SDKs:

### Python SDK
```python
from r2r import R2RClient
client = R2RClient(base_url="http://localhost:7272")
```

### JavaScript SDK
```javascript
const { r2rClient } = require('r2r-js');
const client = new r2rClient("http://localhost:7272");
```

## Important Notes
1. The OpenAI API key is required for the service to function
2. The full deployment requires Docker and Docker Compose
3. The light mode is suitable for testing and development
4. For production use, the full deployment with Docker is recommended

## Documentation Resources
- Official Documentation: https://r2r-docs.sciphi.ai/
- API Documentation: https://r2r-docs.sciphi.ai/self-hosting/installation/overview

## Support
For additional support:
- Join the Discord community: https://discord.gg/p6KqD2kjtB
- Submit issues on GitHub: https://github.com/SciPhi-AI/R2R/issues