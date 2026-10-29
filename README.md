# Back-End-Development-Songs

Flask microservice that serves songs stored in MongoDB.
It is part of the Back-End Development capstone project.

## Endpoints

| Method | Path | Description |
|---|---|---|
| GET | /health | Health check, returns {"status": "OK"} |
| GET | /count | Number of songs |
| GET | /song | List all songs |
| GET | /song/<id> | Get one song (404 if not found) |
| POST | /song | Create a song (302 if the id already exists) |
| PUT | /song/<id> | Update a song (404 if not found) |
| DELETE | /song/<id> | Delete a song (204, or 404 if not found) |

## Configuration

The service reads the MongoDB location from environment variables:

- MONGODB_SERVICE (default: localhost)
- MONGODB_PORT (default: 27017)
- MONGODB_USERNAME and MONGODB_PASSWORD (optional)

On first start, the songs collection is filled from backend/data/songs.json.

## Run locally

    docker run -d --name mongo -p 27017:27017 mongo
    pip install -r requirements.txt
    flask --app backend run -p 5000

## Example requests

    curl -i -X GET localhost:5000/health
    curl -i -X GET localhost:5000/song
    curl -i -X DELETE localhost:5000/song/1

## Deployment

The service is deployed to OpenShift together with a MongoDB deployment
and exposed with `oc expose service/songs`.
