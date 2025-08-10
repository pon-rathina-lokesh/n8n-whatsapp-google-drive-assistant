## 📌 Overview

This project is an n8n automation workflow that listens to WhatsApp messages via Twilio Sandbox and performs file operations in Google Drive.
It supports commands for listing, deleting, and moving — all without leaving WhatsApp.


## ✨ Features

📂 List files in a specified Google Drive folder

🗑 Delete files with confirmation

📦 Move files between folders

📝 Audit log maintained in Google Sheets for safety and traceability

🔒 OAuth2-secured Google Drive access

⚡ Easy deployment via Docker


## 🛠 Tech Stack

n8n – Workflow automation

Twilio Sandbox for WhatsApp – Messaging integration

Google Drive API – File operations

JavaScript Functions – Custom logic in n8n

ngrok – Public URL tunneling for local n8n instance

Docker – Deployment


## ⚙️ Setup Instructions

### 1️⃣ Clone the Repository

git clone https://github.com/pon-rathina-lokesh/n8n-whatsapp-google-drive-assistant.git
cd whatsapp-drive-assistant

### 2️⃣ Environment Variables

Copy .env.sample to .env and fill in the required values:

TWILIO_ACCOUNT_SID=your_twilio_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

### 3️⃣ Twilio Sandbox for WhatsApp Setup

Log in to Twilio Console

Enable WhatsApp Sandbox

Join the sandbox by sending the given code to the Twilio number

Update your .env with your Twilio credentials

Messages sent to the Twilio number will be forwarded to n8n

### 4️⃣ Google Drive API Setup

Go to Google Cloud Console

Create OAuth2 credentials

Enable the Google Drive API

Add your credentials to .env

Authorize the connection from within n8n

### 5️⃣ Running n8n via Docker

docker-compose up -d
Once running, access n8n at:
http://localhost:5678

### 6️⃣ Expose Localhost to Twilio using ngrok

Since Twilio needs a public URL to send webhook requests, use ngrok to expose your local n8n instance:

ngrok http 5678
Copy the generated https://<random>.ngrok.io URL

In your Twilio Sandbox settings, set this URL as the Webhook URL for incoming messages, appending /webhook-path if needed (matching your n8n webhook node path)

### 7️⃣ Import the Workflow

Open n8n

Click Import from File and select workflow.json

Update credentials for:

Twilio

Google Drive

Google Sheets Nodes (for logging)


## 📜 Command Syntax

Command	Description
HELP	Lists the set of commands
LIST	Lists all the folders in the drive
LIST /FolderName	Lists files in /FolderName
DELETE /FolderName/file.pdf   Deletes the specified file. **Requires a `CONFIRM` reply; any other reply will cancel the operation.**
MOVE /FolderName/file.pdf TO /NewFolder	Moves a file to another folder


## 🔍 Workflow Logic

WhatsApp (Twilio) → n8n Webhook → **Code Node (Command Parser)** → **IF Nodes (Routing)** → Google Drive/Sheets API → **Set Node (Format Reply)** → WhatsApp Response


## 📂 Repository Structure
.
├── README.md
├── LICENSE
├── workflow.json
├── .env.sample
├── helper-scripts/
└── docker-compose.yml

## Prerequisites

* Docker and Docker Compose
* ngrok account
* Twilio account
* Google Cloud Platform account


## ⚠️ Safety Features

Confirmation before file deletion

Audit log in Google Sheets

Limited Google Drive scope


## 📹 Demo Video
[![Watch the demo](https://img.youtube.com/vi/D7X3GItou94/0.jpg)](https://youtu.be/D7X3GItou94)


## 📄 License

This project is licensed under the MIT License – see the LICENSE file for details.