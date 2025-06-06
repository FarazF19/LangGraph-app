# LangGraph Ad Analysis App

This repository contains a LangGraph-powered end-to-end pipeline for fetching Facebook ads, extracting and downloading associated videos, transcribing and analyzing them, and generating comprehensive marketing insights. The pipeline leverages OpenAI's Whisper for transcription, GPT-4o for deeper analysis, and stores results locally in structured folders.

---

## Features

* **Facebook Ads Retrieval**: Uses the Meta Graph API to fetch ads for a given ad account.
* **Video URL Extraction**: Parses ad creatives to extract video IDs and fetches their source URLs.
* **Video Download**: Downloads videos locally with proper streaming and error handling.
* **Frame Extraction**: Extracts frames from each video for visual analysis.
* **Audio Transcription**: Transcribes video audio (Urdu) into Urdu script via OpenAI Whisper.
* **Roman Urdu Conversion**: Converts transcription into Roman Urdu using GPT-4o.
* **Transcription Analysis**: Identifies marketing techniques (e.g., emotional storytelling, urgency, risk reversal) via GPT-4o.
* **Frame Analysis**: Performs mock or real visual frame analysis.
* **Final Ad Analysis**: Merges transcription and visual insights to produce a JSON summary with hook, tone, power phrases, and visual highlights.
* **Graph Visualization**: Automatically generates and saves a Mermaid-based PNG of the workflow.

---

## Directory Structure

```
LangGraph-app/
├── ad_analysis/               # Final JSON summaries of ad analysis
├── frame_analysis/            # JSON outputs of visual frame analysis
├── nodes/                     # Individual node implementations
│   ├── get_ads.py             # Fetch Facebook ads
│   ├── get_video_urls.py      # Extract video URLs
│   ├── download_video.py      # Download videos
│   ├── extract_frames.py      # Extract frames
│   ├── transcribe_video.py    # Transcribe videos
│   ├── analyze_transcription.py # Analyze transcripts
│   ├── analyze_frames.py      # Analyze frames
│   └── analyze_ad.py          # Final ad analysis
├── tmp_videos/                # Downloaded videos (input)
├── transcription_analysis/    # JSON outputs of transcription analysis
├── transcriptions/            # Raw transcription text files
├── ad_analysis/               # Final ad analysis JSON files
├── graph.py                   # LangGraph pipeline definition
├── main.py                    # Entry point to run the pipeline
├── .env                       # Environment variables (API keys)
├── requirements.txt           # Python dependencies
└── README.md                  # Project overview (this file)
```

---

## Prerequisites

* Python 3.8+
* [pipenv](https://pipenv.pypa.io/) or `venv` for managing virtual environment
* Meta Facebook Ad account credentials
* OpenAI API key

---

## Setup

1. **Clone this repository**

   ```bash
   git clone https://github.com/yourusername/LangGraph-app.git
   cd LangGraph-app
   ```

2. **Create and activate a virtual environment**

   ```bash
   python -m venv venv
   source venv/bin/activate    # Linux/macOS
   venv\Scripts\activate     # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   Copy `.env.example` to `.env` and fill in your credentials:

   ```env
   # .env
   FB_ACCESS_TOKEN=your_facebook_access_token
   FB_AD_ACCOUNT_ID=act_1234567890
   OPENAI_API_KEY=sk-your-openai-key
   ```

5. **Prepare directories**
   Ensure `tmp_videos/`, `transcriptions/`, `transcription_analysis/`, `frame_analysis/`, and `ad_analysis/` exist (the pipeline will create them if missing).

---

## Usage

Run the entire end-to-end pipeline via:

```bash
python main.py
```

This will:

1. Fetch Facebook ads
2. Extract video URLs
3. Download videos
4. Extract frames
5. Transcribe audio
6. Analyze transcriptions
7. Analyze frames
8. Perform final ad analysis
9. Save results in `ad_analysis/` and graph visualization as `ad_analysis/graph_output.png`

---

## Customization

* **Nodes**: Each step is implemented as a separate node in `nodes/`. You can swap mock implementations (e.g., `analyze_frames`) with real logic.
* **Model Settings**: Change `model` parameters in node scripts to leverage different OpenAI models or local alternatives.
* **Output Formats**: Modify saving logic to export CSV, database writes, or integrate with LangChain-driven dashboards.

---

## License

MIT License. See [LICENSE](LICENSE) for details.
