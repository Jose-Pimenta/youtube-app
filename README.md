# YouTube Clone App

A YouTube-like video streaming platform clone built with **React**, **Vite**, and the **YouTube Data API**.  
[![Vercel](https://img.shields.io/badge/Deploy-on_Vercel-000?style=flat&logo=vercel&logoColor=white)](https://youtube-clone.tiagopimenta.pt)

## Features

- 📺 Browse popular and trending videos
- 🔍 Search for videos by keywords
- 🎥 View detailed video pages with embedded YouTube player
- 📃 Display video metadata: title, description, channel info, view count, likes
- 📋 Related videos sidebar
- 📱 Responsive design for mobile and desktop

## Tech Stack

- **React**
- **Vite**
- **JavaScript (ES6+)**
- **CSS Modules** or **Styled Components**
- **React Router** for client-side routing
- **YouTube Data API v3**
- **ESLint**

## Project Structure

```
youtube-app/
├── public/                      # Static assets (favicons, images)
├── src/
│   ├── components/              # Reusable UI components (Navbar, VideoCard, VideoList, etc.)
│   ├── pages/                   # Page components (Home, SearchResults, VideoDetail)
│   ├── services/                # API request definitions (api.js)
│   ├── App.jsx                  # Root component with routes
│   ├── main.jsx                 # React entry point
│   └── assets/                  # Static media and styles
├── .eslintrc.cjs                # ESLint configuration
├── .gitignore                   # Files and folders to ignore in Git
├── index.html                   # Vite HTML template
├── package.json                 # Project metadata and dependencies
├── vite.config.js               # Vite configuration
└── README.md                    # This file
```

## Prerequisites

- Node.js (v14 or later recommended)
- npm or yarn
- A YouTube Data API key

## Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/Jose-Pimenta/youtube-app.git
   cd youtube-app
   ```

2. **Install dependencies**

   ```bash
   npm install
   # or
   yarn install
   ```

3. **Configure environment variables**  
   Create a `.env` file in the project root with:

   ```
   VITE_YOUTUBE_API_KEY=your_youtube_api_key_here
   ```

   - Sign up at the [Google Developers Console](https://console.developers.google.com/) and enable the YouTube Data API v3 to obtain an API key.

4. **Run the development server**
   ```bash
   npm run dev
   ```
   Open your browser at `http://localhost:5173` (or as shown in console).

## Scripts

- `npm run dev` — Start development server with hot module replacement.
- `npm run build` — Build the production-ready files into `dist/`.
- `npm run serve` — Serve the production build locally for preview (requires `serve` package or similar).
- `npm run lint` — Run ESLint to check and fix code style issues.

## Environment Variables

- `VITE_YOUTUBE_API_KEY`: Your YouTube Data API key.

## Usage

- **Home Page**: Displays popular or trending videos.
- **Search**: Use the search bar in the Navbar to find videos by keywords.
- **Video Detail**: Click a video card to navigate to a detail page showing the embedded YouTube player, video description, channel information, and related videos.
- **Responsive Design**: The layout adjusts for various screen sizes.

## API Service (Example)

In `src/services/api.js`, you may have functions like:

```js
import axios from 'axios';

const BASE_URL = 'https://www.googleapis.com/youtube/v3';

export const fetchPopularVideos = async (apiKey, maxResults = 20) => {
  const response = await axios.get(\`\${BASE_URL}/videos\`, {
    params: {
      part: 'snippet,contentDetails,statistics',
      chart: 'mostPopular',
      regionCode: 'US',
      maxResults,
      key: apiKey,
    },
  });
  return response.data.items;
};

export const searchVideos = async (query, apiKey, maxResults = 20) => {
  const response = await axios.get(\`\${BASE_URL}/search\`, {
    params: {
      part: 'snippet',
      q: query,
      type: 'video',
      maxResults,
      key: apiKey,
    },
  });
  return response.data.items;
};

// Add more functions: fetchVideoById, fetchRelatedVideos, etc.
```

Ensure to handle API quotas and errors gracefully in your components.

## Code Quality

- ESLint is set up; run `npm run lint` to check for issues.
- Follow React best practices for component structure, hooks usage, and state management. Consider using React Query or Redux for more complex state or caching needs.

## Deployment

1. Build the project:
   ```bash
   npm run build
   ```
2. Deploy the contents of the `dist/` folder to a static hosting service (e.g., Vercel, Netlify, GitHub Pages). Ensure environment variable `VITE_YOUTUBE_API_KEY` is set in the deployment environment.

## Additional Resources

- **YouTube Data API Docs**: https://developers.google.com/youtube/v3
- **Vite Documentation**: https://vitejs.dev/
- **React Documentation**: https://reactjs.org/
- **ESLint Documentation**: https://eslint.org/

## Contributing

Contributions are welcome! Please open an issue or submit a pull request with your proposed changes.

- Fork the repository
- Create a new branch: `git checkout -b feature/YourFeature`
- Commit your changes: `git commit -m "Add feature"`
- Push to the branch: `git push origin feature/YourFeature`
- Open a Pull Request

## License

This project is licensed under the MIT License.
