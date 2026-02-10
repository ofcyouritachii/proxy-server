#  Proxy Server

A powerful web-based HTTP proxy server built with Flask. Send HTTP requests through a beautiful web interface with support for custom headers, request bodies, and Discord webhooks.

## Features

✨ **Web Interface** - Beautiful, modern UI for making HTTP requests  
📝 **Custom Headers** - Add any JSON headers to your requests  
💾 **Request Body Support** - Send GET, POST, PUT, PATCH, DELETE, HEAD requests  
🔗 **URL Proxying** - Forward requests to any HTTP/HTTPS endpoint  
📊 **Response Display** - View status codes, headers, and response bodies  
🎯 **Multiple HTTP Methods** - GET, POST, PUT, PATCH, DELETE, HEAD  
📢 **Discord Logging** (Optional) - Log requests to Discord webhooks  
🏥 **Health Check** - Built-in health check endpoint  
📡 **JSON API** - Programmatic API for proxy requests  

## Installation

### Prerequisites
- Python 3.7+
- pip

### Setup

1. **Clone the repository:**
```bash
git clone https://github.com/ofcyouritachii/proxy-server.git
cd proxy-server
```

2. **Create a virtual environment:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies:**
```bash
pip install -r requirements.txt
```

4. **(Optional) Set Discord webhook URL:**
```bash
export DISCORD_WEBHOOK_URL="your-webhook-url-here"
```

## Usage

### Start the server:
```bash
python app.py
```

The server will start on `http://localhost:5000`

### Web Interface
1. Open `http://localhost:5000` in your browser
2. Enter the target URL
3. Select HTTP method
4. Add headers (JSON format) if needed
5. Add request body if needed
6. Click "Send Request"
7. View the response with status code, headers, and body

### API Endpoint

**POST** `/api/proxy`

Request body:
```json
{
  "url": "https://api.example.com/endpoint",
  "method": "POST",
  "headers": {
    "Content-Type": "application/json",
    "Authorization": "Bearer token"
  },
  "body": "{\"key\": \"value\"}"
}
```

Response:
```json
{
  "status": 200,
  "headers": {
    "Content-Type": "application/json",
    ...
  },
  "body": "response content"
}
```

### Health Check

**GET** `/health`

Response:
```json
{
  "status": "healthy",
  "discord": "available"
}
```

## Configuration

### Discord Webhook (Optional)

To enable Discord notifications for proxy requests:

1. Create a Discord webhook in your server
2. Set the environment variable:
```bash
export DISCORD_WEBHOOK_URL="https://discord.com/api/webhooks/YOUR_WEBHOOK_ID/YOUR_WEBHOOK_TOKEN"
```

Discord will receive:
- Failed requests with error details
- Successful requests with status, headers, and response body

## Project Structure

```
proxy-server/
├── app.py                 # Main Flask application
├── requirements.txt       # Python dependencies
├── templates/
│   └── index.html        # Web interface
├── static/
│   └── css/
│       └── style.css     # Styling
├── LICENSE               # License
└── README.md             # This file
```

## Dependencies

- **Flask** - Web framework
- **requests** - HTTP library
- **discord-webhook** - Discord integration (optional)
- **Werkzeug** - WSGI utilities

## Logging

Application logs are printed to console with timestamp and log level. Check the console output when running the server.

Example log output:
```
2025-02-10 12:34:56,789 - INFO - Request ID: a1b2c3d4-e5f6-47g8-h9i0-j1k2l3m4n5o6 | Method: GET | URL: https://api.example.com
```

## Error Handling

The application handles various error scenarios:
- Invalid URL format
- Invalid headers JSON
- Network request failures
- Timeout errors (10-second timeout)
- Discord webhook failures (logged but doesn't stop the proxy)

## Security Notes

⚠️ **Use with caution:**
- This proxy forwards requests without filtering or sanitization
- Sensitive URLs/data passed through the proxy are logged
- Discord webhooks will receive all request/response data
- Consider authentication/authorization for sensitive environments

## Performance

- Request timeout: 10 seconds
- Response size limit: 1000 characters for Discord notifications
- No caching - each request is fresh

## Troubleshooting

**Port 5000 already in use:**
```bash
python app.py  # Change port in app.py or use PORT env variable
```

**Discord webhooks not working:**
- Verify the webhook URL is correct
- Check Discord webhook still exists
- Check network connectivity

**SSL/TLS errors:**
- Ensure Python has up-to-date certificates
- Use urllib3 or requests to handle SSL verification

## Contributing

Feel free to submit issues and enhancement requests!

## License

See LICENSE file for details.

---

**Disclaimer:** This tool is provided as-is for educational and development purposes. Users are responsible for complying with API terms of service and applicable laws when using this proxy.
