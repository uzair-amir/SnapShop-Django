# SnapShop

A full-stack e-commerce price comparison and aggregation web application that helps users search for products, compare prices across multiple online stores, and make informed purchasing decisions.

## Features

- **Product Search** - Search products by text query or barcode/image upload
- **Price Comparison** - Compare prices across multiple Pakistani (.pk) and international (.com) stores
- **Barcode Detection** - Upload product images for automatic barcode scanning using PyZbar
- **Object Detection** - YOLO-based AI fallback when barcode is not detectable
- **User Authentication** - Secure JWT-based authentication system
- **Product Reviews** - Rate and review products (1-5 stars)
- **Store Ratings** - Rate online stores based on experience
- **Wishlist** - Save products for later purchase
- **Recommendations** - Get product recommendations based on store ratings
- **Real-time Price Scraping** - Automated web scraping to fetch current prices

## Tech Stack

### Frontend
- React 18.2.0
- React Router DOM 6.21.0
- Bootstrap 5.3.2
- MDB React UI Kit
- Axios for API calls
- JWT Decode for authentication

### Backend
- Django 5.0.6
- Django REST Framework 3.15.1
- Simple JWT for authentication
- Scrapy 2.11.1 for web scraping
- Selenium 4.20.0 for dynamic content
- OpenCV 4.10.0.84 for image processing
- PyZbar for barcode detection
- Ultralytics (YOLO) 8.2.14 for object detection
- PyTorch 2.3.0 for deep learning

### Database
- SQLite3 (development)

## Project Structure

```
SnapShop/
├── frontend/                 # React application
│   └── src/
│       ├── Pages/           # Page components (Home, Product, Login, etc.)
│       ├── components/      # Reusable components (Hero, Navbar, etc.)
│       ├── context/         # React Context (AuthContext)
│       └── utils/           # Utility functions (PrivateRoute, axios)
│
└── backend/                 # Django project
    ├── api/                 # User authentication & management
    ├── links/               # Google Search API integration
    ├── webstore/            # Product & store management
    ├── pro_scrape/          # Scraped product data storage
    ├── barcode/             # Barcode/object detection
    ├── reviewmark/          # Reviews & wishlist
    ├── selenium_backend/    # Scrapy web scraping
    └── best.pt              # YOLO model file
```

## Installation

### Prerequisites
- Python 3.10+
- Node.js 18+
- npm or yarn

### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file with the following variables:
   ```env
   SECRET_KEY=your-django-secret-key
   GOOGLE_API_KEY=your-google-api-key
   CX=your-google-custom-search-engine-id
   ```

5. Run migrations:
   ```bash
   python manage.py migrate
   ```

6. Start the development server:
   ```bash
   python manage.py runserver
   ```

### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm start
   ```

The frontend will run on `http://localhost:3000` and the backend on `http://127.0.0.1:8000`.

## API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/token/` | User login |
| POST | `/api/register/` | User registration |
| POST | `/api/token/refresh/` | Refresh access token |

### Products & Search
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/search_and_store/` | Search products and store results |
| GET | `/api/get_products/` | Get search results |
| GET | `/api/get_scraped_products/` | Get products with prices |
| GET | `/store/get_product_details/` | Get product details by IDs |

### Barcode Detection
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/file/decode-barcode/` | Upload image for barcode detection |

### Reviews & Ratings
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/store/submit_rating/` | Submit store rating |
| GET | `/store/get_webstore_names/` | Get all store names |
| GET | `/store/get_webstore_ratings/` | Get average store ratings |
| GET | `/store/recommendations/` | Get product recommendations |

### Wishlist
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/mark/add_to_wishlist/` | Add product to wishlist |
| DELETE | `/mark/remove_from_wishlist/{id}/` | Remove from wishlist |

### User Profile
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/get_user_info/` | Get user profile info |
| POST | `/api/update_profile/` | Update user profile |

## How It Works

### Text Search Flow
1. User enters a product search term
2. Application queries Google Custom Search API for `.pk` and `.com` domains
3. Results are stored and Scrapy crawler extracts prices from store websites
4. Prices are displayed for comparison

### Barcode/Image Detection Flow
1. User uploads a product image
2. PyZbar attempts to decode the barcode
3. If no barcode found, YOLO object detection identifies the product
4. Product name is extracted and searched automatically

## Configuration

### Environment Variables

| Variable | Description |
|----------|-------------|
| `SECRET_KEY` | Django secret key |
| `GOOGLE_API_KEY` | Google Custom Search API key |
| `CX` | Google Custom Search Engine ID |

## Screenshots

*Add screenshots of your application here*

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -m 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Open a Pull Request

## License

This project is developed as a Final Year Project (FYP).

## Acknowledgments

- Google Custom Search API for product discovery
- Ultralytics for YOLO object detection
- Scrapy framework for web scraping
