# AI Content Generator Agent

This project demonstrates how to build a **no-code AI Agent** using [Make.com](https://www.make.com/) that automatically fetches the latest AI news, generates a LinkedIn post and Instagram reel script, creates an image, and emails the content to you daily. The workflow uses **OpenAI Assistant**, **Google Gemini**, and **Gmail API** for automation.

---

## 🚀 Features

* Automatically fetches the latest AI news from OpenAI Assistant
* Summarizes and analyzes AI product launches
* Generates:

  * A 150-word Instagram reel script
  * A LinkedIn post caption in an engaging tone
  * An image based on the news
* Emails you the full content daily with the generated image attached

---

## 🧰 Tools Used

| Tool                                           | Purpose                                 |
| ---------------------------------------------- | --------------------------------------- |
| [Make.com](https://www.make.com/)              | Automation workflow platform            |
| [OpenAI Assistant API](https://platform.openai.com) | Fetching latest AI news                 |
| [Google Gemini API](https://ai.google.dev)     | Generating text and images              |
| Gmail API                                      | Sending email with AI-generated content |

---

## 🧩 Workflow Overview

### Step 1: Create a Webhook Trigger

* Log in to Make.com and create a **new scenario**.
* Add a **Webhook module** → Choose **Custom Webhook** → Name it `content_generator_webhook`.
* Save the URL. This will trigger the workflow whenever opened.

### Step 2: Fetch Latest AI News

* Add an **OpenAI Assistant module** → `Create a Message`.
* Connect your **OpenAI API key** from `https://platform.openai.com/api-keys`.
* Configure the assistant to fetch and analyze the latest AI news in JSON format.

### Step 3: Parse JSON Output

* Add **Tools → Compose a String** to format the OpenAI output.
* Then, add **JSON Parser** to extract `title`, `summary`, and `url` fields.

### Step 4: Generate Reel & LinkedIn Post

* Add **Gemini → Create Completion** module.
* Connect your **Gemini API key** from `https://ai.google.dev`.
* Select **Gemini 2.5 Flash model**.
* Configure a prompt to generate an Instagram reel script and LinkedIn post based on the AI news data.

### Step 5: Extract Key Word for Image Generation

* Add another **Gemini → Create Completion** module.
* Configure it to extract a key word from the news summary for image generation.

### Step 6: Generate Image

* Add **Gemini → Create Image** module.
* Use **Image Gen 3.0 model** with a 1:1 aspect ratio.
* Create a prompt that incorporates the extracted keyword into a relevant image.

### Step 7: Send Email with Gmail

* Add **Gmail → Send Email** module.
* Connect your Gmail account.
* Configure the email subject with the news title.
* Set up the email body with HTML formatting to include the generated content and image.
* Attach the image from the image generation module.

### Step 8: Create an AI Agent

* Go to **Make AI Agents → Create New Agent**.
* Name it `Content Specialist`.
* Add the scenario you created as a **System Tool**.
* Save and test your agent.

---

## ⚙️ Automation Schedule

* You can schedule this workflow to run automatically every morning (e.g., 11:00 AM) using the **Scheduler module** in Make.

---

## 📬 Output Example

**Email Output Includes:**

* HTML-formatted AI news summary
* Instagram Reel Script
* LinkedIn Post Caption
* Generated Image (attached)

---

## 📦 Setup Checklist

* [ ] Sign up for [Make.com](https://www.make.com/)
* [ ] Get API key from [OpenAI](https://platform.openai.com/api-keys)
* [ ] Get API key from [Google Gemini](https://ai.google.dev/)
* [ ] Connect your Gmail account
* [ ] Follow workflow steps
* [ ] Test and automate!

---

## 🧠 Future Enhancements

* Auto-post to LinkedIn and Instagram using APIs
* Add video generation for AI reel
* Include trending keyword tracking

