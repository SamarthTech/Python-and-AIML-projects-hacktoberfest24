# Spotify Playlist Randomizer
## Project Description

The **Spotify Playlist Randomizer** is a Python-based project that allows users to create a new Spotify playlist with randomly selected songs from their personal music library. The project uses the Spotipy library, a Python client for the Spotify Web API, to interact with Spotify’s features like accessing saved tracks and creating playlists. The goal is to generate a playlist containing a number of randomly selected tracks from the user’s saved library.

## Prerequisites

Before using the script, make sure you have the following installed and configured:

1. **Python 3.x**: Ensure Python is installed on your system. You can download it from [here](https://www.python.org/downloads/).

2. **Spotipy**: This is a lightweight Python library for the Spotify Web API. Install it using the following command:
   ```bash
   pip install spotipy
   ```

3. **Spotify Developer Account**: You must have a Spotify Developer account and create a new application to generate the necessary credentials (client ID and client secret). Visit the [Spotify Developer Dashboard](https://developer.spotify.com/) to create an app.

4. **Spotify Premium Account**: Accessing specific features of the Spotify API (like modifying playlists) requires a Spotify Premium account.

## Setup
### Step 1: Environment Variables

You will need to set up environment variables for your **Spotify Client ID**, **Client Secret**, and **Redirect URI** in your script. These variables are required for authenticating your Spotify account.

You can either set them in your operating system or directly in the script:

```python
os.environ["SPOTIPY_CLIENT_ID"] = "your_spotify_client_id"
os.environ["SPOTIPY_CLIENT_SECRET"] = "your_spotify_client_secret"
os.environ["SPOTIPY_REDIRECT_URI"] = "http://localhost/"
```

### Step 2: Scopes

The scope defines the permissions your app requires. In this case, the app needs access to your saved songs and the ability to modify your playlists:

```python
scope = 'user-library-read playlist-modify-public'
```

### Step 3: Authenticate the User

The script uses the `spotipy.util.prompt_for_user_token()` method to authenticate the user and generate an access token based on the provided username.

### Step 4: Run the Script

When running the script, pass your **Spotify username** as an argument:
```bash
python main.py <your_spotify_username>
```

If the username isn't provided, the script will print a usage message and exit.

## How It Works

### Random Track Selection
1. The script authenticates the user using the Spotipy library.
2. It then randomly selects songs from the user’s saved tracks. The number of tracks to be selected is determined by the range (set to 50 in this script).
3. A new playlist is generated by replacing the existing tracks of a specified playlist with the randomly selected songs.

### Key Variables
- **username**: This is the username passed as an argument when running the script.
- **token**: This is the authorization token obtained after the user grants access to their Spotify account.
- **library_size**: This is an estimate of the total number of songs in the user’s library. The current implementation assumes this is 50, but you can modify it based on the size of your library.

### Key Functions
- **spotipy.Spotify()**: Initializes a Spotify object to interact with the Spotify API.
- **sp.current_user_saved_tracks()**: Fetches tracks saved by the current user.
- **sp.user_playlist_replace_tracks()**: Replaces the existing tracks of a playlist with a new set of tracks.

### Output
The script outputs the result of the playlist creation process, which confirms whether the new playlist was successfully updated.

## Customization

### Modifying the Number of Tracks
You can adjust the number of random tracks added to the playlist by changing the `range` value in the script:
```python
for a in range(50):  # Adjust this number
```

### Adjusting the Playlist
You can specify the playlist that gets updated by replacing `'playlist_id'` with the actual playlist ID you want to modify.

## Troubleshooting

### 1. "Can't get token for <username>"
This error occurs when the script is unable to authenticate the user. Check if:
- The correct username is provided.
- The Spotify app credentials (client ID, secret, and redirect URI) are correctly set.
- The correct scopes are provided.

### 2. Randomization Issues
If the script is not selecting a diverse set of songs:
- Ensure that the `library_size` variable is set to the approximate size of your library. If the value is too small, the randomization might be limited to a small subset of tracks.

---
