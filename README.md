# Spotify Playlist Sorter (Tinder Style) ✨

A simple web application for sorting Spotify playlists quickly using a "Tinder-like" interface. Keep, ignore, or delete songs with keyboard shortcuts or button clicks, accompanied by full track playback.

**[➡️ View Live Demo Here](https://ipcmf.github.io/SpotifySorter/)** <!-- Replace with your actual GitHub Pages link -->

<!-- Optional: Add a screenshot or GIF -->
<!-- [Insert Screenshot/GIF Here] -->
<!-- Example: ![App Screenshot](link/to/your/screenshot.png) -->

## Concept

This tool helps you clean up and refine your Spotify playlists efficiently. Instead of manually dragging songs or right-clicking, you're presented with each song one by one. You can quickly decide whether to keep it for a new playlist, ignore it, or delete it permanently from the original playlist.

## Features

*   **Spotify Login:** Securely log in using Spotify OAuth (Authorization Code Flow with PKCE).
*   **Playlist Selection:** Choose which of your playlists to sort from a dropdown menu.
*   **Track Display:** Shows the current song's cover art, title, and artist(s).
*   **Full Track Playback (Requires Spotify Premium):** Automatically plays the currently displayed song using the Spotify Web Playback SDK.
*   **Sorting Controls:**
    *   **Keep (Right Arrow / → Button):** Adds the song to a temporary "Kept Songs" list for a new playlist.
    *   **Ignore (Left Arrow / ← Button):** Skips the song, leaving it in the original playlist.
    *   **Delete (Backspace / Delete Button):** **Permanently removes** the song from the *original* playlist being sorted (with confirmation).
*   **"Kept Songs" List:** Sidebar displays songs you've chosen to keep.
    *   Play Button (▶️): Play the full track directly from the list.
    *   Remove Button (🗑️): Remove a song from the "Kept" list before creating the new playlist.
*   **Create New Playlist:** Button to create a new private playlist in your Spotify account containing all the songs from the "Kept Songs" list.
*   **Progress Indicator:** Shows which track number you're on and the percentage sorted.

## Tech Stack

*   HTML5
*   CSS3
*   Vanilla JavaScript (ES6+)
*   Spotify Web API (for fetching playlists, tracks, user data, modifying playlists)
*   Spotify Web Playback SDK (for controlling playback in the browser - requires Premium)

## Setup & Usage

**❗ IMPORTANT: Spotify Premium is REQUIRED for the track playback feature to work.**

1.  **Visit the Live Demo:** Go to the link provided above.
2.  **Login:** Click the "Login with Spotify" button.
3.  **Authorize:** You'll be redirected to Spotify to grant permissions. This app requires permissions to:
    *   Read your private playlists (`playlist-read-private`)
    *   Read collaborative playlists (`playlist-read-collaborative`)
    *   Modify your public playlists (`playlist-modify-public`) - *Only needed if you make created playlists public*
    *   Modify your private playlists (`playlist-modify-private`) - *Needed to create the new sorted playlist and delete tracks*
    *   Stream and control playback (`streaming`, `user-read-playback-state`, `user-modify-playback-state`) - *Required by the Web Playback SDK*
    *   Read your user profile (`user-read-private`) - *Needed to identify you for playlist creation*
4.  **Select Playlist:** Choose the playlist you want to sort from the dropdown.
5.  **Sort:**
    *   Use the `←` (Ignore) or `→` (Keep) buttons or the corresponding Arrow Keys.
    *   Use the `Delete` button or `Backspace` key to remove the song from the original playlist (confirm the prompt!).
    *   The current song will automatically play (if you have Premium).
6.  **Manage Kept List:** Use the ▶️ and 🗑️ buttons in the sidebar to manage the songs you've decided to keep.
7.  **Create Playlist:** When ready, click the "Make New Playlist" button in the sidebar, give it a name, and it will be added to your Spotify account.

## Local Development

If you want to run this project locally:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/<your-username>/<your-repo-name>.git
    cd <your-repo-name>
    ```
2.  **Create a Spotify App:**
    *   Go to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/).
    *   Create a new application.
3.  **Configure Redirect URI:**
    *   In your Spotify App settings, add a Redirect URI. For local testing, you need to use a local web server. Add `http://localhost:PORT/` or `http://127.0.0.1:PORT/` (replace `PORT` with the port your server will use, e.g., `8080`, `5500`). Make sure the URL exactly matches what your local server provides.
    *   Enable the "Web Playback SDK" toggle in your Spotify App settings.
4.  **Get Client ID:**
    *   Copy the `Client ID` from your Spotify App dashboard.
    *   Open the `index.html` file.
    *   Find the line `const CLIENT_ID = "YOUR_CLIENT_ID_HERE";` and replace the placeholder with your actual Client ID.
5.  **Run a Local Server:** You *cannot* simply open the `index.html` file directly using `file:///...` due to OAuth Redirect URI restrictions. Use a simple local web server.
    *   **Using VS Code:** Install the "Live Server" extension, right-click `index.html`, and choose "Open with Live Server". Note the port it uses (e.g., 5500) and make sure `http://127.0.0.1:5500/` (or similar) is in your Spotify Redirect URIs.
    *   **Using Python:** Navigate to the project directory in your terminal and run `python -m http.server 8080` (or another port). Make sure `http://localhost:8080/` is in your Spotify Redirect URIs.
    *   **Using Node.js:** Install `http-server` (`npm install -g http-server`) and run `http-server . -p 8080` in the project directory. Make sure `http://localhost:8080/` is in your Spotify Redirect URIs.
6.  **Access:** Open your browser and navigate to the local server address (e.g., `http://localhost:8080`).

## Important Notes

*   **Spotify Premium Required:** Full track playback relies on the Web Playback SDK, which only functions for users logged in with active Spotify Premium subscriptions.
*   **Client ID:** The Spotify Client ID is embedded in the `index.html`. While necessary for this client-side application using PKCE, be aware that it is publicly visible. The more sensitive Client Secret is *not* used or exposed.
*   **Token Expiration:** The access token obtained from Spotify typically expires after 1 hour. This simple implementation does not handle automatic token refreshing. You may need to log in again after the token expires.
*   **Rate Limiting:** Excessive use (sorting extremely rapidly or handling huge playlists very quickly) might potentially hit Spotify API rate limits. The app includes basic batching for adding tracks to minimize this.

## Contributing

Pull requests are welcome! If you have suggestions or improvements, feel free to fork the repo and submit a PR.

## License

[MIT](LICENSE) <!-- Optional: Add a LICENSE file (e.g., MIT License) -->
