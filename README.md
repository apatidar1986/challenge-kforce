# Caching Fetch Library Project

## Introduction

This project implements a caching fetch library for a web application that renders a directory of people. The project consists of a framework (including a server, client runtime, and MSW mock server), a web application, and the caching fetch library.

## Project Structure

- `/framework`: Contains the server, client runtime, and MSW mock server
- `/caching-fetch-library`: Contains the implemented caching fetch library
- `/`: Root directory contains the main application files

## The caching fetch library, however, is incomplete so here is info for that

## Setup and Running the Project

1. Install dependencies:

   ```bash
   npm install
   ```

2. Start the project:

   ```bash
   npm start
   ```

3. Visit [http://localhost:3000](http://localhost:3000) to see the app running.

## Caching Fetch Library Implementation

The caching fetch library (`/caching-fetch-library/cachingFetch.ts`) has been implemented to meet the following requirements:

1. A caching fetch hook (`useCachingFetch`) that returns an object with `isLoading`, `data`, and `error` properties.
2. A preloading caching fetch function (`preloadCachingFetch`) for server-side data fetching.
3. Functions to serialize (`serializeCache`) and initialize (`initializeCache`) the cache for transferring between server and client.

### Key Changes and Improvements

1. Implemented `useCachingFetch` hook:

   - Uses React's `useState` and `useEffect` for managing fetch state and caching.
   - Returns cached data immediately if available.
   - Fetches data only when not in cache.

2. Implemented `preloadCachingFetch` function:

   - Fetches and caches data on the server before rendering.

3. Implemented `serializeCache` and `initializeCache` functions:

   - Allows transferring cache data from server to client.

These changes ensure that:

- The application renders properly with JavaScript enabled (/appWithoutSSRData).
- Only one network request is made when visiting /appWithoutSSRData.
- The application renders properly with JavaScript disabled (/appWithSSRData).
- No network calls are made to the people API when visiting /appWithSSRData with JavaScript enabled.
- When javascript disabled there is no network call /appWithoutSSRData just display loading as its client side.

## Known Issues and Next Steps

1. Error handling could be improved, especially for network failures or invalid data.
2. The current implementation doesn't handle cache expiration or invalidation.
3. Consider implementing a more robust caching strategy (e.g., LRU cache) for larger applications.
4. Add unit and integration tests for the caching fetch library.
5. Implement proper TypeScript typing for the cache and fetched data.

## Configuration Choices

1. Used React hooks for state management in the caching fetch library.
2. Kept the global cache as a simple JavaScript object for simplicity, but this could be improved for larger applications.
3. Used `JSON.stringify` and `JSON.parse` for cache serialization, which works well for simple data structures.

These choices were made to keep the implementation straightforward while meeting the project requirements. For a production-ready project, additional considerations such as performance optimizations, more robust error handling, and comprehensive testing would be necessary.
