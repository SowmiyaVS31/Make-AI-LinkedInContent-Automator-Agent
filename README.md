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
* Use the prompt:

  ```json
  Find and analyze the most important AI tool or product launched in the last 4-5 days.
  Respond only in valid JSON format like:
  {
    "title": "",
    "summary": "",
    "url": ""
  }
  ```

### Step 3: Parse JSON Output

* Add **Tools → Compose a String** to format the OpenAI output.
* Then, add **JSON Parser** to extract `title`, `summary`, and `url` fields.

### Step 4: Generate Reel & LinkedIn Post

* Add **Gemini → Create Completion** module.
* Connect your **Gemini API key** from `https://ai.google.dev`.
* Select **Gemini 2.5 Flash model**.
* Use this prompt structure:

  ```text
  Act like a top-tier content strategist.
  Today's AI News:
  Title: {{title}}
  Summary: {{summary}}
  URL: {{url}}

  Write a 150-word Instagram reel script in the style of a tech influencer.
  Then, write a LinkedIn caption starting with a bold one-liner and ending with a question.
  Return output in HTML format for email with headings: Reel Script, LinkedIn Post, and Source Link.
  ```

### Step 5: Extract Key Word for Image Generation

* Add another **Gemini → Create Completion** module.
* Use prompt:

  ```text
  Based on the following AI news, return one word representing the main topic:
  {{summary}}
  ```

### Step 6: Generate Image

* Add **Gemini → Create Image** module.
* Use **Image Gen 3.0 model** with a 1:1 aspect ratio.
* Prompt example:

  ```text
  A Lego-style image of a person with a laptop. The keyword '{{word}}' appears on their T-shirt and screen.
  ```

### Step 7: Send Email with Gmail

* Add **Gmail → Send Email** module.
* Connect your Gmail account.
* **Subject:** `Today's Top AI News - {{title}}`
* **Body:**

  ```html
  <h2>Today's AI Content</h2>
  {{Gemini HTML output}}
  <img src="cid:ai_image" alt="AI News Image" />
  ```
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

