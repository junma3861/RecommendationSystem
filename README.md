# Product Recommendation System

A collaborative filtering-based recommendation system that suggests products to customers based on their purchase history and similar user behaviors.

## Architecture Overview

### Databases
- **User Profile (SQL)**: Stores user demographic and account information
- **Product (SQL)**: Contains product catalog with details
- **User Purchase History (MongoDB)**: Stores transaction data (ideal for flexible, document-based purchase records with varying attributes)

### Algorithm
- **Collaborative Filtering**: Implements both user-based and item-based approaches
  - User-based: Recommends products liked by similar users
  - Item-based: Recommends products similar to those the user has purchased

## Project Structure

```
recommendation_system/
├── config/
│   └── database.py          # Database connection configuration
├── models/
│   └── schemas.py            # Database schema definitions
├── services/
│   ├── data_loader.py        # Data loading utilities
│   └── collaborative_filtering.py  # CF algorithms
├── recommendation_engine.py  # Main recommendation service
├── example.py               # Usage examples
└── requirements.txt         # Dependencies
```

## Installation

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your database credentials
```

3. Initialize databases with sample data (optional):
```bash
python example.py
```

## Usage

```python
from recommendation_engine import RecommendationEngine

# Initialize the engine
engine = RecommendationEngine()

# Get recommendations for a user
recommendations = engine.get_recommendations(
    user_id=123,
    method='user-based',  # or 'item-based'
    n_recommendations=10
)

print(recommendations)
```

## Features

- **User-based Collaborative Filtering**: Finds similar users based on purchase patterns
- **Item-based Collaborative Filtering**: Finds similar products based on user interactions
- **Cosine Similarity**: Measures similarity between users/items
- **Scalable Data Storage**: SQL for structured data, MongoDB for flexible purchase records

## Why MongoDB for Purchase History?

Purchase history benefits from MongoDB because:
- Flexible schema for varying transaction attributes
- Easy to store nested data (multiple items per purchase)
- Efficient for high-volume write operations
- Natural fit for time-series purchase data
- Simple to add new fields without migrations
