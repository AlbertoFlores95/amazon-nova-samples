# Nova Sonic Tool Use with MP3 Recording

This enhanced version of the Nova Sonic tool use sample includes automatic MP3 recording of assistant responses.

## Features

- **Automatic MP3 Recording**: Assistant responses are automatically recorded and saved as MP3 files
- **Timestamped Files**: Each recording is saved with a timestamp in the filename
- **Organized Storage**: All MP3 files are saved in an `assistant_responses` directory

## Installation

1. Install the required dependencies:
```bash
pip install -r requirements.txt
```

2. Make sure you have ffmpeg installed (required for MP3 encoding):
   - **macOS**: `brew install ffmpeg`
   - **Ubuntu/Debian**: `sudo apt-get install ffmpeg`
   - **Windows**: Download from https://ffmpeg.org/download.html

   **Note**: If ffmpeg is not available, the application will automatically save files as WAV format instead.

## Usage

Run the application as usual:
```bash
python nova_sonic_tool_use.py
```

The application will now automatically:
1. Start recording when the assistant begins speaking
2. Stop recording when the assistant finishes speaking
3. Save the recording as an MP3 file in the `assistant_responses` directory

## Output

Audio files are saved with the naming convention:
```
assistant_responses/assistant_response_YYYYMMDD_HHMMSS.mp3
```

Example: `assistant_responses/assistant_response_20241201_143052.mp3`

**Note**: If ffmpeg is not available, files will be saved as WAV format instead:
```
assistant_responses/assistant_response_YYYYMMDD_HHMMSS.wav
```

## File Structure

```
console-python/
├── nova_sonic_tool_use.py          # Main application with MP3 recording
├── requirements.txt                 # Python dependencies
├── README_MP3_Recording.md         # This file
└── assistant_responses/            # Directory where MP3 files are saved
    ├── assistant_response_20241201_143052.mp3
    ├── assistant_response_20241201_143105.mp3
    └── ...
```

## How It Works

1. **Detection**: The application detects when the assistant starts and stops speaking by monitoring the Bedrock stream events
2. **Recording**: Audio data is captured in real-time during assistant responses
3. **Conversion**: Raw audio data is converted to WAV format, then to MP3 using ffmpeg
4. **Storage**: MP3 files are saved with timestamps for easy identification
5. **Fallback**: If ffmpeg is not available, files are saved as WAV format

## Troubleshooting

- **No audio files created**: Ensure ffmpeg is installed and accessible in your PATH for MP3 conversion
- **WAV files instead of MP3**: This means ffmpeg is not available - the application will still save audio as WAV files
- **Audio quality issues**: The audio files use the same quality as the original audio stream (24kHz, 16-bit, mono)
- **Permission errors**: Ensure the application has write permissions to create the `assistant_responses` directory

## Dependencies

- `pyaudio`: Audio input/output handling
- `pytz`: Timezone handling
- `aws_sdk_bedrock_runtime`: AWS Bedrock integration
- `ffmpeg`: Audio codec support (system dependency, optional - falls back to WAV if not available)
