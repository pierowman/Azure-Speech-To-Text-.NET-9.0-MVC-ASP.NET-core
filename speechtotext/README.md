# Speech to Text with Diarization

This ASP.NET Core MVC application provides a web interface for uploading audio files and transcribing them using Azure Speech Service with speaker diarization.

## Features

- Audio file upload (WAV, MP3, OGG, FLAC)
- Speech-to-text transcription using Azure Cognitive Services
- Speaker diarization (identifies different speakers)
- Real-time progress indication
- Organized results display by speaker segments
- Full transcript view

## Prerequisites

1. .NET 9 SDK
2. Azure Subscription
3. Azure Speech Service resource

## Setup Instructions

### 1. Create Azure Speech Service Resource

1. Go to [Azure Portal](https://portal.azure.com)
2. Create a new **Speech Service** resource
3. Copy the **Key** and **Region** from the resource

### 2. Configure the Application

Update the Azure Speech Service credentials in `appsettings.json` or `appsettings.Development.json`:

```json
{
  "AzureSpeech": {
    "SubscriptionKey": "YOUR_AZURE_SPEECH_KEY",
    "Region": "YOUR_AZURE_REGION"
  }
}
```

Replace:
- `YOUR_AZURE_SPEECH_KEY` with your Azure Speech Service key
- `YOUR_AZURE_REGION` with your Azure region (e.g., "eastus", "westus2")

**Alternative: Using User Secrets (Recommended for Development)**

For better security, use .NET User Secrets:

```bash
dotnet user-secrets set "AzureSpeech:SubscriptionKey" "YOUR_KEY_HERE"
dotnet user-secrets set "AzureSpeech:Region" "YOUR_REGION_HERE"
```

### 3. Run the Application

```bash
cd speechtotext
dotnet restore
dotnet build
dotnet run
```

The application will be available at `https://localhost:5001` (or the port shown in console).

## Usage

1. Open the application in your browser
2. Click "Choose File" and select an audio file
3. Click "Transcribe" to start the process
4. Wait for the transcription to complete
5. View results in either:
   - **Speaker Segments**: See each speaker's contributions with timestamps
   - **Full Transcript**: View the complete conversation

## Supported Audio Formats

- WAV (recommended for best quality)
- MP3
- OGG
- FLAC

**Note**: WAV files provide the best compatibility with Azure Speech Service. For other formats, you may need to convert them to WAV first.

## Best Practices

1. **Audio Quality**: Use clear audio recordings for best results
2. **File Size**: Keep files under 10MB for faster processing
3. **Format**: WAV format at 16kHz sample rate works best
4. **Multiple Speakers**: Ensure speakers are clearly distinguishable
5. **Language**: Currently configured for English (en-US), can be changed in `SpeechToTextService.cs`

## Troubleshooting

### "Subscription key not found" Error
- Check that your appsettings.json has the correct keys
- Verify the configuration section name is "AzureSpeech"

### "Invalid audio format" Error
- Convert your audio to WAV format
- Ensure the file is not corrupted

### No speakers detected
- Azure Speech Service diarization works best with clear audio
- Ensure there are at least 2 distinct speakers
- Try increasing audio quality

## Project Structure

```
speechtotext/
??? Controllers/
?   ??? HomeController.cs          # Handles file upload and API calls
??? Models/
?   ??? ErrorViewModel.cs          # Error handling
?   ??? TranscriptionResult.cs     # Transcription data models
??? Services/
?   ??? SpeechToTextService.cs     # Azure Speech Service integration
??? Views/
?   ??? Home/
?       ??? Index.cshtml            # Main UI
??? appsettings.json                # Configuration
```

## License

This project is for demonstration purposes.
