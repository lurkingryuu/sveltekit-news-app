# NewsApp - Inter IIT Tech Meet 12.0 - IIT KGP Development Team Selection Task

## How to Run Locally?

1. ### Using Docker

   - Clone the repository
   - Navigate to the root directory
   - Run `docker run -p 8888:8888 -d lurkingryuu/devtask_svelte`
   - Navigate to `localhost:8888` to view the app

2. ### Without Docker

   - Clone the repository

     #### Setting up the frontend

     - Install nodejs and npm
     - Run `npm install` to install all the dependencies
     - Run `npm run dev` to start the backend server

## Problem Statement

- Clean and responsive front-end
- Should contain a search bar for headlines and keywords
- A news entity should have the following features:
  - Headline
  - Content
  - Image
  - Video (playback optional)
- Real time news feed
  - Extensive web scraping is not required. Simply ensure that the coming feed conveys a sense of freshness.
- Filtering options for
  - Geographic location
  - Topics (eg. Sports, Politics, Technology, Finance etc.)
- Newsletter subscription service
  - Email can be stored in your choice of database or data-structure

## Remaining Features to Be Implemented

1. Video Integration in the News Section

   - Unfortunately, the utilized news API does not furnish video content.

2. Topic-based Filtering and Search Capability

   - Regrettably, I was unable to implement filtering due to time limitations and the incompatibility of lunr.js with SvelteKit.

3. Newsletter Subscription Functionality
   - The backend successfully handles subscription and unsubscription operations, but the mailing service is not functional, preventing the implementation of the newsletter subscription service.
