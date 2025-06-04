# FastAPI Installation and Testing Process

This document outlines the process of installing and testing FastAPI, a modern, high-performance web framework for building APIs with Python.

## Installation Process

### 1. Clone the Repository

```bash
git clone https://github.com/tiangolo/fastapi.git
cd fastapi
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate
```

### 3. Install FastAPI and Dependencies

FastAPI can be installed directly from the cloned repository in development mode:

```bash
pip install -e .
```

For testing, additional dependencies are needed:

```bash
pip install -r requirements-tests.txt
```

## Testing the Installation

### 1. Basic API Testing

#### Create a Simple FastAPI Application

Create a file named `main.py` with the following content:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get('/')
async def root():
    return {'message': 'Hello World'}
```

#### Run the Application

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

#### Test the API

Once the server is running, you can test it using `curl` or any HTTP client:

```bash
curl http://localhost:8000/
```

Expected response:
```json
{"message": "Hello World"}
```

### 2. Advanced API Features Testing

#### Create an Advanced Application

Create a file with more advanced FastAPI features:

```python
from fastapi import FastAPI, Query, Path, Body
from pydantic import BaseModel, Field
from typing import Optional, List

app = FastAPI(title='Advanced FastAPI Test')

class Item(BaseModel):
    name: str
    description: Optional[str] = None
    price: float
    tax: Optional[float] = None
    tags: List[str] = []

@app.get('/')
async def root():
    return {'message': 'Advanced FastAPI Test'}

@app.get('/items/{item_id}')
async def read_item(item_id: int = Path(..., title='The ID of the item to get'), 
                   q: Optional[str] = Query(None, max_length=50)):
    return {'item_id': item_id, 'q': q}

@app.post('/items/')
async def create_item(item: Item):
    return item

@app.put('/items/{item_id}')
async def update_item(item_id: int, item: Item, importance: int = Body(...)):
    return {'item_id': item_id, 'item': item, 'importance': importance}
```

#### Testing Path Parameters

```bash
curl "http://localhost:8001/items/5?q=test"
```

Response:
```json
{"item_id": 5, "q": "test"}
```

#### Testing POST with JSON Body

```bash
curl -X POST "http://localhost:8001/items/" \
  -H "Content-Type: application/json" \
  -d '{"name": "Foo", "price": 42.0, "tags": ["bar", "baz"]}'
```

Response:
```json
{
    "name": "Foo",
    "description": null,
    "price": 42.0,
    "tax": null,
    "tags": ["bar", "baz"]
}
```

#### Testing PUT with Nested JSON

```bash
curl -X PUT "http://localhost:8001/items/5" \
  -H "Content-Type: application/json" \
  -d '{"item": {"name": "Bar", "price": 50.2}, "importance": 5}'
```

Response:
```json
{
    "item_id": 5,
    "item": {
        "name": "Bar",
        "description": null,
        "price": 50.2,
        "tax": null,
        "tags": []
    },
    "importance": 5
}
```

### 3. Explore API Documentation

FastAPI automatically generates interactive API documentation:

- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc
- OpenAPI JSON Schema: http://localhost:8000/openapi.json

## Features Verified

- ✅ Installation from GitHub repository
- ✅ Basic application startup
- ✅ API endpoint functionality
- ✅ JSON response generation
- ✅ Path parameters handling
- ✅ Query parameters handling
- ✅ Request body validation with Pydantic models
- ✅ Data validation and serialization
- ✅ Nested JSON handling
- ✅ Auto-generated documentation available
- ✅ OpenAPI schema generation

## Key Components of FastAPI

- **Starlette**: FastAPI builds on Starlette for the web parts
- **Pydantic**: Used for data validation, serialization, and documentation
- **Uvicorn**: ASGI server used to run FastAPI applications
- **OpenAPI**: For API documentation generation

## System Requirements

- Python 3.7+
- Dependencies automatically installed through pip

## Notes

- FastAPI is an ASGI framework and requires an ASGI server like Uvicorn or Hypercorn to run
- For production deployment, consider using Gunicorn with Uvicorn workers
- The framework is very performant, on par with NodeJS and Go for API services
- The automatic data validation using Pydantic models provides great developer experience and runtime safety