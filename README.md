## Backend Setup

### 1. Set Up Python Virtual Environment
```bash
cd backend
source venv/bin/activate
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure Database

#### PostgreSQL
1. Create a PostgreSQL database:
```bash
createdb happydb
```
2. Add schema:
```bash
CREATE TABLE app_users (
    id SERIAL PRIMARY KEY,
    device_id TEXT UNIQUE NOT NULL
);

CREATE TABLE happiness_surveys (
    app_user_id INTEGER REFERENCES app_users(id),
    id SERIAL PRIMARY KEY,
    current_activity VARCHAR(255) NOT NULL,
    happiness_level SMALLINT CHECK (happiness_level BETWEEN 1 AND 5),
    submitted_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE subscriptions (
    app_user_id INTEGER REFERENCES app_users(id),
    id SERIAL PRIMARY KEY,
    subscribed BOOLEAN DEFAULT FALSE,
    last_response_at TIMESTAMP WITH TIME ZONE
);
```

### 5. Run Database Migrations
```bash
cd happybackend
python manage.py makemigrations
python manage.py migrate
```

### 6. Create Superuser (Optional)
```bash
python manage.py createsuperuser
```

### 7. Run the Development Server
```bash
python manage.py runserver
```

## Testing

### Run Django Server Tests
```bash
cd happybackend
python manage.py test
```

### Run iOS App Tests
#### 1. Open Xcode
#### 2. Go to personInfoSwiftUITests/personInfoSwiftUITests.swift
#### 3. Press Cmd+U to run the tests

## Database Management

### Access PostgreSQL Shell
```bash
psql -U happy_user -d happydb
```

## iOS App Setup

### 1. Configure API Endpoint
Update the base URL in your iOS app to point to your Django server:
```swift
let baseURL = "http://localhost:8000/api/"
```

## Development Workflow

### 1. Start Backend
```bash
cd backend
source venv/bin/activate
cd happybackend
python manage.py runserver  
```

### 2. Build and Run iOS app

### Common Issues

#### Database Connection Error
- Ensure PostgreSQL is running
- Verify database credentials in settings.py
- Check if database exists

#### iOS Network Error
- Ensure Django server is running
- Check API base URL in iOS app
- Verify network permissions in iOS app

## Project Structure

```
smile-/
├── backend/
│   ├── happybackend/
│   │   ├── api/
│   │   │   ├── models.py          # Database models
│   │   │   ├── views.py           # API endpoints
│   │   │   ├── serializers.py     # Data serialization
│   │   │   ├── urls.py            # URL routing
│   │   │   └── tests.py           # Test suite
│   │   ├── happybackend/
│   │   │   ├── settings.py        # Django settings
│   │   │   └── urls.py            # Main URL configuration
│   │   └── manage.py              # Django management script
│   ├── requirements.txt           # Python dependencies
│   └── venv/                      # Virtual environment
├── ios/                           # iOS application
└── README.md                      # This file
```
