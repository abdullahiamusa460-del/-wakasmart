# WakaSmart Development Setup

## Prerequisites

- Python 3.9+ or Node.js 16+
- Flutter SDK (for mobile development)
- Git
- Docker (optional, for containerized development)
- PostgreSQL 13+
- Redis 6+

## Backend Setup

### 1. Clone Repository

```bash
git clone https://github.com/abdullahiamusa460-del/wakasmart.git
cd wakasmart
```

### 2. Python Backend (FastAPI)

```bash
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Edit .env with your configuration

# Initialize database
python scripts/init_db.py

# Run migrations
alembic upgrade head

# Start development server
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### 3. Database Setup

```bash
# Create database
createdb wakasmart_dev

# Create PostgreSQL user (if needed)
createuser wakasmart_user -P

# Grant privileges
psql -c "ALTER USER wakasmart_user CREATEDB;"
```

### 4. Redis Setup (for caching and job queue)

```bash
# Using Docker (recommended)
docker run -d -p 6379:6379 redis:latest

# Or install locally and start
redis-server
```

## Frontend Setup

### 1. Flutter Mobile App

```bash
cd mobile

# Get Flutter packages
flutter pub get

# Run on emulator/device
flutter run

# Build APK (Android)
flutter build apk

# Build IPA (iOS)
flutter build ios
```

### 2. Web Dashboard (if applicable)

```bash
cd frontend

# Install Node dependencies
npm install

# Start development server
npm start

# Build for production
npm run build
```

## ML/Computer Vision Setup

```bash
cd ml

# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install ML dependencies
pip install -r requirements.txt

# Download pre-trained models
python scripts/download_models.py

# Start model serving
python serving.py
```

## Running Tests

### Backend Tests

```bash
cd backend

# Run all tests
pytest

# Run with coverage
pytest --cov=src

# Run specific test file
pytest tests/test_routes.py
```

### Mobile Tests

```bash
cd mobile

# Run tests
flutter test

# Run with coverage
flutter test --coverage
```

## Environment Variables

Create a `.env` file in the project root:

```bash
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/wakasmart_dev
REDIS_URL=redis://localhost:6379

# API Configuration
API_HOST=0.0.0.0
API_PORT=8000
DEBUG=True

# Authentication
JWT_SECRET_KEY=your-secret-key-here
JWT_ALGORITHM=HS256

# AWS/S3 (for image storage)
AWS_ACCESS_KEY_ID=your-key
AWS_SECRET_ACCESS_KEY=your-secret
AWS_S3_BUCKET=wakasmart-uploads
AWS_REGION=us-east-1

# ML Model Configuration
MODEL_PATH=models/road_classifier.pb
CV_API_ENDPOINT=http://localhost:8001

# Third-party APIs
MAPBOX_TOKEN=your-token
```

## Useful Commands

### Git Workflow

```bash
# Create feature branch
git checkout -b feature/your-feature-name

# Make changes and commit
git add .
git commit -m "feat: Add your feature"

# Push to GitHub
git push origin feature/your-feature-name
```

### Code Quality

```bash
# Format code
black .

# Lint
flake8 .

# Type checking
mypy .
```

## Troubleshooting

### Database Connection Error
- Ensure PostgreSQL is running: `pg_isready`
- Check DATABASE_URL in .env
- Verify database user has correct permissions

### Redis Connection Error
- Ensure Redis is running: `redis-cli ping`
- Check REDIS_URL in .env

### Flutter Build Error
- Run `flutter clean`
- Run `flutter pub get`
- Check Flutter version: `flutter --version`

## Questions?

Create an issue or check existing documentation!

---

**Happy coding!** 🚀
