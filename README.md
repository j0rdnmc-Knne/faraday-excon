# URLShort ![build](https://github.com/url-tools/shortener/workflows/CI/badge.svg) ![python](https://img.shields.io/badge/python-3.8%2B-blue)

Lightweight URL shortening with PostgreSQL. Minimal dependencies.

## Quick Setup

```bash
# Create and activate virtual environment
python -m venv env
source env/bin/activate

# Install dependencies
pip install -r requirements.txt

# Database setup
python manage.py makemigrations
python manage.py migrate

# Start development server
python manage.py runserver
```

Access the application at `http://localhost:8000`

## Features

- **Custom short codes** - Generate memorable URLs
- **Analytics tracking** - Click statistics and referrer data  
- **API endpoints** - RESTful interface for integration
- **Bulk operations** - Process multiple URLs efficiently
- **Expiration policies** - Automatic link cleanup
- **QR code generation** - Mobile-friendly sharing

## Configuration

Environment variables:
```bash
export DATABASE_URL=postgresql://user:pass@localhost/urlshort
export SECRET_KEY=your-secret-key-here
export DEBUG=False
```

## Production Deployment

```bash
# Collect static files
python manage.py collectstatic

# Gunicorn setup
gunicorn urlshort.wsgi:application --bind 0.0.0.0:8000

# With nginx reverse proxy
# See deployment/nginx.conf for configuration
```

## API Usage

```bash
# Create short URL
curl -X POST http://localhost:8000/api/links/ \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com", "custom_code": "demo"}'

# Response: {"short_url": "http://localhost:8000/demo"}
```

## Database Schema

- **Links** - Original URLs, short codes, creation dates
- **Clicks** - Visit timestamps, IP addresses, user agents  
- **Users** - Account management with API keys

## Performance

- Handles 1000+ requests per second
- Sub-5ms response time for redirects
- Efficient index usage for lookups

## Monitoring

Built-in health checks at `/health/` and metrics at `/metrics/` (Prometheus format).

## License

MIT License - see LICENSE file for details.

# PR Update: 2025-12-01 12:23:11
