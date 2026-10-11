# Wanderlust

Wanderlust is a travel-stay listing app built with Express, MongoDB, and server-rendered EJS pages. Browse stays by destination or category, view listing details and map locations, and sign in to create and manage listings or leave reviews.

## Features

- Search listings by title or location
- Browse categories including trending, rooms, iconic cities, mountains, castles, pools, camps, farms, and arctic stays
- Create, edit, and delete listings with Cloudinary-hosted images
- Register and sign in with local username/password authentication
- Add star ratings and comments to listings
- View listing locations on a map

## Requirements

- Node.js `22.13.1` (as specified in `package.json`)
- MongoDB, available through MongoDB Atlas or a local instance
- Cloudinary credentials for listing image uploads
- An OpenRouteService API key for geocoding listing locations

## Setup

1. Install dependencies:

   ```bash
   npm install
   ```

2. Create a `.env` file in the project root:

   ```dotenv
   ATLASDB_URL=mongodb+srv://<username>:<password>@<cluster>/<database>
   SECRETE=replace-with-a-long-random-session-secret
   CLOUD_NAME=your-cloudinary-cloud-name
   CLOUD_API_KEY=your-cloudinary-api-key
   CLOUD_API_SECRET=your-cloudinary-api-secret
   OPENROUTEKEY=your-openrouteservice-api-key
   ```

   `ATLASDB_URL` can also point to a local MongoDB instance. Keep real credentials private; `.env` is excluded from Git.

3. Start the app:

   ```bash
   node app.js
   ```

4. Open [http://localhost:8080](http://localhost:8080).

The server connects to the configured MongoDB database when it starts. The app listens on port `8080`.

## Main routes

| Route | Purpose |
| --- | --- |
| `GET /listings` | Browse, search, and filter listings |
| `GET /listings/:id` | View listing details, reviews, and map |
| `GET /listings/new` | Open the new-listing form (sign-in required) |
| `POST /listings` | Create a listing (sign-in required) |
| `GET /signup` | Register an account |
| `GET /login` | Sign in |
| `POST /listings/:id/reviews` | Add a review (sign-in required) |

Listing owners can edit or delete their own listings. Signed-in users can delete reviews they authored.

## Project structure

```text
controllers/       Listing, review, and user request handlers
models/            Mongoose models for listings, reviews, and users
routes/            Express routes and static CSS/JavaScript
views/             EJS pages and shared layout partials
init/              Development data initialization utilities
app.js             Express app setup and server entry point
cloudConfig.js     Cloudinary image storage configuration
middleware.js      Authentication, ownership, and validation middleware
```

## Development notes

- The `npm test` script is currently a placeholder; no automated tests are configured.
- The data initialization utility in `init/` is intended for development. Review its database target and external-service configuration before running it.
- Never commit API keys, database credentials, or session secrets. If a key has been exposed, revoke or rotate it with its provider.
