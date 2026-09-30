Deployed Link:
https://macrosnap-bhaskarudu.streamlit.app/
# AI Vision Nutrition Chatbot 🍱

An AI-powered nutrition assistant that can analyze a photo of a meal, identify the food items, provide estimated nutritional information, and answer follow-up questions about the meal.

The application also summarizes the conversation and allows the user to send the summary directly to WhatsApp.

This project was built to explore how multimodal AI, external APIs, conversational AI, and cloud deployment can be combined into a practical application.

---

## 📌 Overview

Tracking nutrition usually requires manually identifying the food, checking portion sizes, and searching for nutritional information.

This project makes that process simpler.

A user can upload a photo of their meal, and the application uses **Google Gemini's multimodal capabilities** to analyze the image and provide an estimated breakdown of the meal.

After the initial analysis, the user can continue chatting with the AI and ask questions such as:

* "Is this meal high in protein?"
* "What are the main sources of carbohydrates?"
* "How can I make this meal healthier?"
* "What should I reduce if I want fewer calories?"

Once the conversation is complete, the user can generate a summary and send it to WhatsApp.

---

## ✨ Features

### 🖼️ Meal Image Analysis

Upload a photo of a meal and let Gemini analyze the image.

The AI can identify visible food items and provide an estimated nutritional breakdown.

### 🥗 Nutrition Estimation

The application generates estimated values such as:

* Calories
* Protein
* Carbohydrates
* Fat
* Other relevant nutritional information

The values are AI-generated estimates and should not be treated as medically accurate measurements.

### 💬 AI Conversation

After the image is analyzed, users can continue the conversation with the AI.

For example:

```text
User:
Is this meal good for a high-protein diet?

AI:
The meal contains several protein sources, particularly
from the chicken and dal. Based on the estimated portion,
it provides approximately 35g of protein.
```

### 📝 Conversation Summary

The application can summarize the conversation into a short and readable format.

The summary can include:

* Food identified
* Estimated nutrition
* Important observations
* User questions
* AI recommendations

### 📱 WhatsApp Integration

The generated summary can be sent to the user's WhatsApp using the **Twilio WhatsApp API**.

### ☁️ Cloud Deployment

The application is designed to run as a Streamlit application and can be deployed using **Streamlit Community Cloud**.

---

# 🏗️ Application Workflow

The overall workflow looks like this:

```text
                User
                 │
                 ▼
        ┌─────────────────┐
        │   Streamlit UI  │
        └────────┬────────┘
                 │
                 │ Upload Meal Image
                 ▼
        ┌─────────────────┐
        │  Google Gemini  │
        │  Vision Model   │
        └────────┬────────┘
                 │
                 ▼
        Food & Nutrition
           Analysis
                 │
                 ▼
        ┌─────────────────┐
        │  AI Chatbot     │
        └────────┬────────┘
                 │
                 │ Conversation
                 ▼
        ┌─────────────────┐
        │ Conversation     │
        │ Summary          │
        └────────┬────────┘
                 │
                 ▼
        ┌─────────────────┐
        │  Twilio API     │
        │  WhatsApp       │
        └────────┬────────┘
                 │
                 ▼
              WhatsApp
```

---

# 🧰 Technologies Used

| Technology                | Purpose                                    |
| ------------------------- | ------------------------------------------ |
| Python                    | Main programming language                  |
| Streamlit                 | Web application and user interface         |
| Google Gemini API         | Image analysis and conversational AI       |
| Twilio WhatsApp API       | Sending summaries to WhatsApp              |
| Git & GitHub              | Version control and source code management |
| Streamlit Community Cloud | Application deployment                     |

---

# 📁 Project Structure

The project is organized to keep the UI, AI processing, and external integrations separate.

```text
ai-vision-nutrition-chatbot/
│
├── app.py
│
├── services/
│   ├── gemini_service.py
│   ├── whatsapp_service.py
│   └── summary_service.py
│
├── utils/
│   ├── prompts.py
│   └── validators.py
│
├── requirements.txt
├── README.md
├── .gitignore
└── .env
```

### `app.py`

The main Streamlit application.

It handles the user interface, image upload, user interaction, and connects the different services together.

### `services/gemini_service.py`

Contains the logic for communicating with the Google Gemini API.

It is responsible for:

* Sending the meal image to Gemini
* Generating the initial meal analysis
* Handling follow-up questions

### `services/whatsapp_service.py`

Handles communication with the Twilio WhatsApp API.

It is responsible for sending the generated conversation summary to the user's WhatsApp.

### `services/summary_service.py`

Handles the generation of a concise summary from the conversation.

### `utils/prompts.py`

Contains the prompts used to guide Gemini's responses.

Keeping prompts separately makes them easier to modify and test.

### `utils/validators.py`

Contains validation logic for user inputs and uploaded files.

---

# ⚙️ How It Works

## 1. Upload a Meal Image

The user uploads an image through the Streamlit interface.

```text
Meal Image
     ↓
Streamlit
```

The application validates the uploaded file before processing it.

---

## 2. Send Image to Gemini

The image is passed to Google's Gemini multimodal model along with a prompt describing the required analysis.

For example, the model is instructed to:

```text
Identify the food items in the image.

Estimate the nutritional information.

Provide a clear explanation of the result.

Mention that nutritional values are estimates.
```

---

## 3. Generate Meal Analysis

Gemini processes both the image and the prompt and returns the analysis.

A typical response might contain:

```text
Food Identified:
- Rice
- Chicken
- Dal
- Salad

Estimated Nutrition:
Calories: ~650 kcal
Protein: ~35 g
Carbohydrates: ~75 g
Fat: ~20 g
```

---

## 4. Continue the Conversation

The user can ask questions based on the analyzed meal.

For example:

```text
User:
Is this meal high in protein?

AI:
The meal appears to provide a moderate to high amount
of protein, mainly from chicken and dal.
```

The conversation context is maintained so that follow-up questions can refer to the previously analyzed meal.

---

## 5. Generate a Summary

When the user finishes the conversation, the application generates a concise summary.

Example:

```text
Meal:
Chicken, rice, dal and salad

Estimated Calories:
~650 kcal

Estimated Protein:
~35 g

Summary:
The meal provides a good source of protein from chicken
and dal along with carbohydrates from rice.
```

---

## 6. Send Summary to WhatsApp

The summary is passed to the Twilio WhatsApp API.

```text
Application
     │
     ▼
Twilio WhatsApp API
     │
     ▼
User's WhatsApp
```

The user receives the meal summary without having to manually copy it from the web application.

---

# 🔐 Environment Variables

API credentials should not be hard-coded into the application.

Create a `.env` file locally:

```env
GEMINI_API_KEY=your_gemini_api_key

TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TWILIO_WHATSAPP_NUMBER=your_twilio_whatsapp_number
```

The actual values should never be committed to GitHub.

Add `.env` to `.gitignore`:

```gitignore
.env
__pycache__/
*.pyc
```

---

# 🚀 Getting Started

## Prerequisites

Before running the project, make sure you have:

* Python 3.9+
* A Google Gemini API key
* A Twilio account
* Twilio WhatsApp configuration
* Git

---

## 1. Clone the Repository

```bash
git clone https://github.com/your-username/ai-vision-nutrition-chatbot.git
```

Move into the project directory:

```bash
cd ai-vision-nutrition-chatbot
```

---

## 2. Create a Virtual Environment

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### macOS / Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Configure Environment Variables

Create a `.env` file in the root directory.

```env
GEMINI_API_KEY=your_key_here
TWILIO_ACCOUNT_SID=your_sid_here
TWILIO_AUTH_TOKEN=your_auth_token_here
TWILIO_WHATSAPP_NUMBER=your_whatsapp_number_he_
```

