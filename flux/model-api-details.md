# FLUX.1-schnell Integration Details

## About the Model

**Model**: [`black-forest-labs/FLUX.1-schnell`](https://huggingface.co/black-forest-labs/FLUX.1-schnell)  
**Type**: Text-to-Image generation  
**Available via**:  
- **EURI API** (recommended for faster, managed access)  
- **Hugging Face Inference API** (alternative, official source)

---

## Using the EURI API

EURI provides a streamlined API to access the FLUX.1-schnell model with added benefits such as better performance and easier authentication.

### How to Get Access

1. Visit the [EURI website](https://euron.one)  
2. Sign up and create an account  
3. Generate your EURI API key from the dashboard

### API Endpoint
POST https://api.euron.one/api/v1/euri/images/generations


### Authentication

Pass your API key in the headers:

```http
Authorization: Bearer YOUR_API_TOKEN
Content-Type: application/json
{
  "prompt": "A beautiful sunset over mountains",
  "model": "black-forest-labs/FLUX.1-schnell",
  "n": 2,
  "size": "1024x1024",
  "quality": "standard",
  "response_format": "url",
  "style": "vivid"
}
```

Parameters explained:
- prompt: Your text description of the image to generate
- model: The model identifier (black-forest-labs/FLUX.1-schnell)
- n: Number of images to generate
- size: Resolution of generated images (e.g., "512x512", "1024x1024")
- quality: Image quality preset ("standard" or "high")
- response_format: Format of the response, either "url" or "base64"
- style: Style preset (e.g., "vivid", "photorealistic", etc.)

### Example cURL Request

curl -X POST https://api.euron.one/api/v1/euri/images/generations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -d '{
    "prompt": "A beautiful sunset over mountains",
    "model": "black-forest-labs/FLUX.1-schnell",
    "n": 2,
    "size": "1024x1024",
    "quality": "standard",
    "response_format": "url",
    "style": "vivid"
  }'
  
### Response

The API responds with JSON containing the generated image URLs, for example:
{
  "created": 1696000000,
  "data": [
    {"url": "https://cdn.euron.one/generated/abc123.png"},
    {"url": "https://cdn.euron.one/generated/def456.png"}
  ]
}

---

## Alternative: Hugging Face Inference API
If you prefer not to use EURI, you can use the official Hugging Face API, though it might have slower response times and stricter rate limits.

### API Endpoint
POST https://api-inference.huggingface.co/models/black-forest-labs/FLUX.1-schnell

### Authentication
- Use your Hugging Face API token:
- Authorization: Bearer YOUR_HF_TOKEN
- Content-Type: application/json

Request Body Format
{
  "inputs": "a futuristic city with flying cars",
  "parameters": {
    "negative_prompt": "blurry, low quality"
  }
}

### Response
Depending on the setup, you might receive:
- A direct binary image response
- A base64 encoded image string
- A URL pointing to the generated image


---

# How to Use in n8n

## Using EURI API in HTTP Request Node
- Method: POST
- URL: https://api.euron.one/api/v1/euri/images/generations
- Authentication: Bearer Token (your EURI API key)
- Headers:
{
  "Content-Type": "application/json",
  "Authorization": "Bearer YOUR_API_TOKEN"
}
- Body:
{
  "prompt": "={{$json['message']['text']}}",
  "model": "black-forest-labs/FLUX.1-schnell",
  "n": 1,
  "size": "1024x1024",
  "quality": "standard",
  "response_format": "url",
  "style": "vivid"
}


## Using Hugging Face API in HTTP Request Node
- Method: POST
- URL: https://api-inference.huggingface.co/models/black-forest-labs/FLUX.1-schnell
- Authentication: Bearer Token (your Hugging Face API token)
- Headers:
{
  "Content-Type": "application/json",
  "Authorization": "Bearer YOUR_HF_TOKEN"
}
- Body:
{
  "inputs": "={{$json['message']['text']}}"
}