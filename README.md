&lt;p align="center">
&lt;img src="https://media.giphy.com/media/v1.gif" alt="TDS Virtual TA Logo" width="150" height="150">
&lt;/p>

📚 TDS Virtual TA: Your AI-Powered IITM Course Assistant 🤖

 



&lt;p align="center">
&lt;img src="https://media.giphy.com/media/v1.gif" alt="Animated AI Assistant" width="300" height="200">
&lt;br>
&lt;i>"Never get stuck on a Tools in Data Science question again!"&lt;/i>
&lt;/p>

✨ Project Overview
Welcome to the TDS Virtual TA! This project aims to revolutionize the learning experience for IIT Madras Online Degree students enrolled in the "Tools in Data Science" course. Tired of waiting for TA responses? Our intelligent AI-powered assistant provides instant, accurate answers to your course-related queries, leveraging both official course content and the collective knowledge from the TDS Discourse forum.

This project is built as a highly responsive API, designed to handle student questions, even those with image attachments, and provide comprehensive answers along with relevant links to the source material.

🎯 Key Features
Intelligent Q&amp;A: Answers student questions about the "Tools in Data Science" course content.
Discourse Integration: Leverages historical Discourse posts (Jan 1, 2025 - Apr 14, 2025) for richer, community-driven insights.
Course Content Integration: Incorporates official TDS Jan 2025 course content (as on Apr 15, 2025).
Multimodal Input (Image Support): Accepts questions with optional Base64 encoded image attachments for visual queries.
Contextual Responses: Provides concise answers with clickable links to the source (Discourse threads, course materials).
Fast & Responsive: Designed to deliver responses within 30 seconds.
Robust Data Scraping: Includes scripts to efficiently gather data from Discourse using session keys.
Advanced Data Processing: Converts scraped data into optimized chunks, embeddings, and stores them in a robust database for RAG (Retrieval Augmented Generation).
🚀 Getting Started
Follow these steps to set up and run your very own TDS Virtual TA!

📋 Prerequisites
Before you begin, ensure you have the following installed:

Python 3.9+
pip (Python package installer)
An IITM account with access to the TDS Discourse forum (for data scraping).
An AI Proxy API key (e.g., OpenAI, configured as an environment variable).
📦 Installation
Clone the Repository:

Bash

git clone https://github.com/YOUR_USERNAME/tds-virtual-ta.git
cd tds-virtual-ta
Install Dependencies:

Bash

pip install -r requirements.txt
⚙️ Configuration
Environment Variables:
Set your AI Proxy API key as an environment variable. Replace YOUR_AI_PROXY_KEY with your actual key.

Bash

export AI_PROXY_KEY="YOUR_AI_PROXY_KEY"
(For Windows, use set AI_PROXY_KEY=YOUR_AI_PROXY_KEY in Command Prompt or $env:AI_PROXY_KEY="YOUR_AI_PROXY_KEY" in PowerShell).

📊 Data Preparation
The scraper directory contains scripts to gather the necessary data.

Scrape Data from Discourse:
You'll need your IITM Discourse session key for this step.

Bash

cd scraper
python scrap.py --session-key "YOUR_IITM_SESSION_KEY"
This script will download Discourse threads into the downloaded_threads folder (JSON format) and relevant course content into the md_downloaded folder (Markdown format).

Preprocess Data & Create Database:
The preprocess.py script takes the raw downloaded data, cleans it, chunks it, creates embeddings, and stores it in a database optimized for RAG.

Bash

cd .. # Navigate back to the root directory
python preprocess.py
This will populate the data/ directory with your processed data.

🏃 Running the API
Once the data is prepared and environment variables are set, you can run the API using uvicorn.

Bash

uvicorn api.app:app --host 0.0.0.0 --port 8000 --reload
Your API will now be live at http://0.0.0.0:8000 (or http://localhost:8000).
You can access the interactive API documentation at http://localhost:8000/docs.

&lt;p align="center">
&lt;img src="https://media.giphy.com/media/v1.gif" alt="API Demo GIF" width="400" height="250">
&lt;br>
&lt;i>(Imagine a GIF here showing the /docs endpoint with a sample request and response)&lt;/i>
&lt;/p>

💡 API Usage
The API exposes a POST endpoint to answer student questions.

Endpoint: /api/ (assuming your app is hosted at https://app.example.com)

Request (JSON):

JSON

{
  "question": "Should I use gpt-4o-mini which AI proxy supports, or gpt3.5 turbo?",
  "image": "Optional base64 encoded image string"
}
Example curl request with an image:

Bash

curl "https://app.example.com/api/" \
  -H "Content-Type: application/json" \
  -d "{\"question\": \"Should I use gpt-4o-mini which AI proxy supports, or gpt3.5 turbo?\", \"image\": \"$(base64 -w0 project-tds-virtual-ta-q1.webp)\"}"
(Note: base64 -w0 is for Linux/macOS. For Windows, you might need a different method or tool to get the base64 string.)

Response (JSON):

JSON

{
  "answer": "You must use `gpt-3.5-turbo-0125`, even if the AI Proxy only supports `gpt-4o-mini`. Use the OpenAI API directly for this question.",
  "links": [
    {
      "url": "https://discourse.onlinedegree.iitm.ac.in/t/ga5-question-8-clarification/155939/4",
      "text": "Use the model that’s mentioned in the question."
    },
    {
      "url": "https://discourse.onlinedegree.iitm.ac.in/t/ga5-question-8-clarification/155939/3",
      "text": "My understanding is that you just have to use a tokenizer, similar to what Prof. Anand used, to get the number of tokens and multiply that by the given rate."
    }
  ]
}
✅ Evaluation
We utilize promptfoo for comprehensive evaluation of the API's performance.

Configure promptfoo:
Edit promptfoo.yaml and replace providers[0].config.url with your deployed API URL (e.g., https://app.example.com/api/).

Run Evaluation:

Bash

npx -y promptfoo eval --config promptfoo.yaml
This will run a set of sample questions against your API and provide an evaluation report.

&lt;p align="center">
&lt;img src="https://media.giphy.com/media/v1.gif" alt="Evaluation GIF" width="400" height="250">
&lt;br>
&lt;i>(Visualize a GIF showing the promptfoo evaluation running and a snippet of the results)&lt;/i>
&lt;/p>

☁️ Deployment
You can deploy this application to any public URL of your choice (e.g., Render, Heroku, AWS, Google Cloud, Azure). Ensure your API endpoint is publicly accessible for evaluation.

(Consider adding a small badge or icon for recommended deployment platforms here.)

🤝 Contributing
We welcome contributions to enhance the TDS Virtual TA! If you have suggestions, bug reports, or want to contribute code, please feel free to:

Fork the repository.
Create a new branch (git checkout -b feature/your-feature).
Make your changes.
Commit your changes (git commit -m 'feat: Add new awesome feature').
Push to the branch (git push origin feature/your-feature).
Open a Pull Request.
📜 License
This project is licensed under the MIT License - see the LICENSE file for details.

📧 Contact
For any questions or inquiries, please open an issue on this repository.

&lt;p align="center">
&lt;img src="https://media.giphy.com/media/v1.gif" alt="Thank You GIF" width="100" height="100">
&lt;/p>

