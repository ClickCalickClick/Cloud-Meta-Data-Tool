# AI Image Tagger - Cloud Meta Data Tool

An intelligent, browser-based tool that automatically generates and embeds AI-powered metadata into your JPEG images using Google Cloud Vision API. Process single images or entire folders in batch mode, with the ability to review and edit metadata before downloading.

## 🌟 Features

- **Batch Processing**: Process multiple images or entire folders at once
- **AI-Powered Metadata**: Automatically generates:
  - Natural language captions
  - Relevant keywords
  - Object detection with confidence scores
  - OCR text extraction
- **Editable Metadata**: Review and customize AI-generated descriptions before finalizing
- **Privacy-Focused**: All processing happens in your browser; your API key is stored locally
- **No Server Required**: Completely client-side application
- **Automatic Metadata Embedding**: Metadata is written directly into JPEG EXIF data

## 🚀 Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Safari, or Edge)
- A Google Cloud Vision API key (see instructions below)

### Installation

1. Download or clone this repository
2. Open `cloud-meta-data-tool.html` in your web browser
3. Configure your Google Cloud Vision API key (see below)

That's it! No installation or dependencies required.

## 🔑 How to Generate a Google Cloud Vision API Key

Follow these steps to obtain your API key:

### Step 1: Create a Google Cloud Account

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Sign in with your Google account (or create one if needed)
3. Accept the terms of service if prompted

### Step 2: Create a New Project

1. Click on the project dropdown at the top of the page
2. Click **"New Project"**
3. Enter a project name (e.g., "Image Tagger")
4. Click **"Create"**
5. Wait for the project to be created, then select it from the project dropdown

### Step 3: Enable the Vision API

1. In the Google Cloud Console, open the navigation menu (☰)
2. Go to **"APIs & Services"** > **"Library"**
3. Search for **"Cloud Vision API"**
4. Click on **"Cloud Vision API"** in the results
5. Click the **"Enable"** button
6. Wait for the API to be enabled (this may take a minute)

### Step 4: Create API Credentials

1. Go to **"APIs & Services"** > **"Credentials"**
2. Click **"Create Credentials"** at the top
3. Select **"API key"**
4. Your API key will be created and displayed in a popup
5. **Important**: Click **"Restrict Key"** to secure your API key:
   - Under "API restrictions", select "Restrict key"
   - Choose "Cloud Vision API" from the dropdown
   - Click **"Save"**
6. Copy your API key - you'll need it for the next step

### Step 5: Configure the Tool

1. Open the AI Image Tagger tool in your browser
2. Click the **Settings (⚙️)** icon in the top-right corner
3. Paste your API key into the text field
4. Click **"Save Key"**

Your API key is now saved and ready to use!

## 💾 Where is the API Key Stored?

### localStorage Location

The API key is stored in your browser's **localStorage** with the key name: `googleApiKey`

### Storage Details

- **Location**: The key is stored in your browser's localStorage, which is specific to the domain/file where the tool is running
- **Privacy**: The data never leaves your computer except when making API calls to Google Cloud Vision
- **Persistence**: The key remains stored until you:
  - Clear your browser's localStorage/cache
  - Manually delete it from localStorage
  - Use a different browser or device

### How to View or Delete Your Stored API Key

You can access localStorage through your browser's Developer Tools:

#### Chrome / Edge:
1. Press `F12` or right-click and select "Inspect"
2. Go to the **"Application"** tab
3. In the left sidebar, expand **"Storage"** > **"Local Storage"**
4. Click on the file/domain URL
5. Look for the key named `googleApiKey`
6. To delete: Right-click the key and select "Delete"

#### Firefox:
1. Press `F12` or right-click and select "Inspect Element"
2. Go to the **"Storage"** tab
3. Expand **"Local Storage"**
4. Click on the file/domain URL
5. Look for the key named `googleApiKey`
6. To delete: Right-click the key and select "Delete Item"

#### Safari:
1. Enable Developer Tools: Safari > Preferences > Advanced > Show Develop menu
2. Right-click and select "Inspect Element"
3. Go to the **"Storage"** tab
4. Select **"Local Storage"**
5. Click on the file/domain URL
6. Look for the key named `googleApiKey`

### Security Note

Your API key is stored in plain text in localStorage. To keep it secure:
- Don't share your browser profile or localStorage data
- Use API key restrictions in Google Cloud Console (limit to Vision API only)
- Set up billing alerts in Google Cloud Console
- Regularly rotate your API keys
- Never commit your API key to version control

## 📖 How to Use the Tool

### Basic Workflow

1. **Configure API Key** (one-time setup)
   - Click the Settings icon (⚙️)
   - Enter your Google Cloud Vision API key
   - Click "Save Key"

2. **Select Images**
   - Click **"Choose Images"** to select individual JPEG files, or
   - Click **"Choose Folder"** to process an entire folder of images

3. **Start Processing**
   - Click **"Start Processing"**
   - Wait for the AI to analyze each image
   - Progress will be displayed for each file

4. **Review & Edit (Optional)**
   - Click **"Review & Edit Metadata"** to expand the review panel
   - Edit captions and keywords as desired
   - Changes are applied when you download

5. **Download Results**
   - For single images: Downloads the tagged image directly
   - For multiple images: Downloads a ZIP file containing all tagged images
   - Metadata is embedded in the EXIF data of each JPEG

### File Naming

Processed images are renamed with the suffix `-ai-meta-data` before the file extension:
- Original: `vacation.jpg`
- Tagged: `vacation-ai-meta-data.jpg`

## 🛠️ Technical Details

### Technologies Used

- **Frontend**: HTML5, CSS3 (Tailwind CSS), Vanilla JavaScript
- **Image Processing**: piexif.js for EXIF metadata manipulation
- **Compression**: JSZip for creating downloadable archives
- **AI Service**: Google Cloud Vision API

### Metadata Fields

The tool writes metadata to the following EXIF fields:
- **ImageDescription** (0th IFD): Contains the AI-generated caption and keywords
- **UserComment** (Exif IFD): Duplicate of the description for compatibility

### API Features Used

The tool utilizes these Google Vision API features:
- **Label Detection**: Identifies general image content
- **Object Localization**: Detects specific objects with bounding boxes
- **Text Detection (OCR)**: Extracts visible text from images
- **Web Detection**: Finds similar images and web entities

### Supported File Formats

- **Input**: JPEG images only (`.jpg`, `.jpeg`)
- **Output**: JPEG images with embedded EXIF metadata

## ❓ Troubleshooting

### "Please set your Google Vision API key in Settings"

**Solution**: You need to configure your API key. Click the Settings icon and enter your key.

### "Failed to call Google Vision API"

**Possible causes**:
1. Invalid API key - Verify your key in Google Cloud Console
2. Vision API not enabled - Make sure you enabled the Cloud Vision API
3. API quota exceeded - Check your Google Cloud Console for quota limits
4. Network issues - Check your internet connection

### "No JPEG files found in the selection"

**Solution**: The tool only supports JPEG images. Make sure you're selecting `.jpg` or `.jpeg` files.

### API Key Not Saving

**Possible causes**:
1. Browser localStorage is disabled - Check your browser's privacy settings
2. Private/Incognito mode - localStorage may not persist in private browsing
3. Browser security settings - Some browsers may block localStorage for local files

**Solution**: Try opening the file with a local web server:
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Node.js (with http-server package)
npx http-server
```

Then access the tool at `http://localhost:8000/cloud-meta-data-tool.html`

### Processing Takes a Long Time

**Explanation**: Each image requires an API call to Google Cloud Vision. Processing time depends on:
- Number of images
- Image file sizes
- Your internet connection speed
- Google API response time

**Tip**: Start with a small batch to test, then process larger batches once you're familiar with the tool.

## 💰 Cost Information

Google Cloud Vision API is a paid service, but includes a free tier:
- **Free**: 1,000 images per month
- **Paid**: After free tier, pricing varies by feature used

For current pricing details, visit the [Google Cloud Vision API Pricing page](https://cloud.google.com/vision/pricing).

**Recommendation**: Set up billing alerts in Google Cloud Console to monitor usage.

## 🔒 Privacy & Security

- **Client-Side Only**: All image processing happens in your browser
- **No Data Collection**: Your images are never uploaded to any server except Google's Vision API
- **API Key Storage**: Stored locally in your browser only
- **Open Source**: Full source code is available for inspection

## 📝 License

This project is provided as-is for educational and personal use.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page.

## 📧 Support

If you encounter any issues or have questions, please open an issue on the GitHub repository.

---

**Note**: This tool requires an active internet connection to communicate with Google Cloud Vision API. The API key and processed images are handled entirely in your browser for maximum privacy.
