# Node.js Express API with MongoDB

This is a containerized Node.js Express application that provides API endpoints for dealership and review data using MongoDB as the backend database.

## Prerequisites

- Docker Desktop (must be running)
- Node.js (for local testing)

## API Endpoints

The application provides the following endpoints:

### Review Endpoints
- `GET /fetchReviews` - Fetch all reviews
- `GET /fetchReviews/dealer/:id` - Fetch reviews for a specific dealer by ID
- `POST /insert_review` - Insert a new review

### Dealership Endpoints  
- `GET /fetchDealers` - Fetch all dealerships
- `GET /fetchDealers/:state` - Fetch dealerships by state
- `GET /fetchDealer/:id` - Fetch a specific dealer by ID

## Setup and Running

### Using Docker (Recommended)

1. Ensure Docker Desktop is running
2. Navigate to the database directory:
   ```bash
   cd server/database
   ```

3. Build the Docker image:
   ```bash
   docker build . -t nodeapp
   ```

4. Run the application with docker-compose:
   ```bash
   docker-compose up
   ```

The application will be available at `http://localhost:3030`

### For Local Development (Without Docker)

1. Install dependencies:
   ```bash
   npm install
   ```

2. Start the application:
   ```bash
   node app.js
   ```

## Testing the Endpoints

You can test the endpoints using curl or any HTTP client:

### Test Examples:

1. **Fetch Reviews for Dealer 29:**
   ```bash
   curl http://localhost:3030/fetchReviews/dealer/29
   ```

2. **Fetch All Dealerships:**
   ```bash
   curl http://localhost:3030/fetchDealers
   ```

3. **Fetch Dealer by ID 3:**
   ```bash
   curl http://localhost:3030/fetchDealer/3
   ```

4. **Fetch Dealerships in Kansas:**
   ```bash
   curl http://localhost:3030/fetchDealers/Kansas
   ```

## Data Structure

### Dealership Schema
```javascript
{
  id: Number,
  city: String,
  state: String,
  address: String,
  zip: String,
  lat: String,
  long: String,
  short_name: String,
  full_name: String
}
```

### Review Schema
```javascript
{
  id: Number,
  name: String,
  dealership: Number,
  review: String,
  purchase: Boolean,
  purchase_date: String,
  car_make: String,
  car_model: String,
  car_year: Number
}
```

## Implementation Details

- Uses Express.js for the web server
- MongoDB for data storage with Mongoose ODM
- CORS enabled for cross-origin requests
- Body parser for handling request data
- Docker containerization for easy deployment

## Files Structure

- `app.js` - Main application file with all endpoints
- `dealership.js` - Mongoose schema for dealerships
- `review.js` - Mongoose schema for reviews
- `data/dealerships.json` - Sample dealership data
- `data/reviews.json` - Sample review data
- `Dockerfile` - Docker configuration
- `docker-compose.yml` - Docker Compose configuration
- `package.json` - Node.js dependencies 