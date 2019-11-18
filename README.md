Domain Short App

## Table of Contents
* [Key Features](#key-features)
* [Stack](#stack)
* [Setup](#setup)
* [API](#api)
* [Contributing](#contributing)

## Key Features
* Free and open source.
* Custom domain support.
* Custom URLs for shortened links
* Setting password for links.
* Private statistics for shortened URLs.
* View and manage your links.
* RESTful API.

## Stack
* Node (Web server)
* Express (Web server framework)
* Passport (Authentication)
* React (UI library)
* Next (Universal/server-side rendered React)
* Redux (State management)
* styled-components (CSS styling solution library)
* Recharts (Chart library)
* Neo4j (Graph database)

## Setup
You need to have [Node.js](https://nodejs.org/), [Neo4j](https://neo4j.com/) and [Redis](https://redis.io/) installed on your machine.

1. Clone this repository.
2. Copy `config.example.js` to `config.js` in both server and client folders and fill them properly.
3. Install dependencies: `npm install`.
4. Start Neo4j database.
5. Run for development: `npm run dev`.
6. Run for production: `npm run build` then `npm start`.

**Docker:** You can use Docker to run the app. Read [docker-examples](/docker-examples) for more info.

## API
In addition to the website, you can use these APIs to create, delete and get URLs.

### Types

```
URL {
  createdAt {string} ISO timestamp of when the URL was created
  id {string} Unique ID of the URL
  target {string} Where the URL will redirect to
  password {boolean} Whether or not a password is required
  count {number} The amount of visits to this URL
  shortUrl {string} The shortened link (Usually https://kutt.it/id)
}
```

In order to use these APIs you need to generate an API key from settings. Never put this key in the client side of your app or anywhere that is exposed to others.

All API requests and responses are in JSON format.

Include the API key as `X-API-Key` in the header of all below requests. Available API endpoints with body parameters:

**Get shortened URLs list:**
```
GET /api/url/geturls
```

Returns:
```
{
  list {Array<URL>} List of URL objects
  countAll {number} Amount of items in the list
}
```

**Submit a link to be shortened**:
```
POST /api/url/submit
```
Body:
  * `target`: Original long URL to be shortened.
  * `customurl` (optional): Set a custom URL.
  * `password` (optional): Set a password.
  * `reuse` (optional): If a URL with the specified target exists returns it, otherwise will send a new shortened URL.

Returns: URL object

**Delete a shortened URL** and **Get stats for a shortened URL:**
```
POST /api/url/deleteurl
GET /api/url/stats
```
Body (or query for GET request)
  * `id`: ID of the shortened URL.
  * `domain` (optional):  Required if a custom domain is used for short URL.
  
## Contributing
Pull requests are welcome. You'll probably find lots of improvements to be made.

Open issues for feedback, requesting features, reporting bugs or discussing ideas.

