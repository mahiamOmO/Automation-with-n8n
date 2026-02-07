# Facebook Messenger Automation with n8n

This README explains how to create a **Facebook Messenger automation** using **Facebook Developer App + n8n** step by step.

---

## 1. Facebook App Creation

### Step 1: Create Developer Account

* Go to: [https://developers.facebook.com/](https://developers.facebook.com/)
* Login with your Facebook account
* Accept developer terms

### Step 2: Create a New App

* Click **My Apps → Create App**
* Choose **Business** (recommended for Messenger automation)
* Fill in:

  * App Name
  * App Contact Email
* Click **Create App**

---

## 2. Facebook App Setup & App Live

### Add Messenger Product

* Go to **Add Product**
* Select **Messenger**
* Click **Set Up**

### Generate Page Access Token

* Connect your Facebook Page
* Generate **Page Access Token**
* Save it securely (you will need it in n8n)

### App Live Mode

* Go to **App Settings → Basic**
* Fill required info:

  * Privacy Policy URL
  * Terms of Service URL
  * App Icon
* Switch **App Mode: Development → Live**

---

## 3. Send Data to n8n Webhook & Get Activation Info

### Create Webhook in n8n

* Create a new workflow
* Add **Webhook Node**
* Set:

  * HTTP Method: `POST`
  * Path: `/facebook-webhook`
* Copy the **Production Webhook URL**

### Use Webhook URL in Facebook App

* This URL will be used as:

  * Callback URL
  * Webhook receiver

### Data You Will Receive

From Facebook, n8n webhook will receive:

* Sender ID (PSID)
* Message Text
* Timestamp
* Page ID

---

## 4. Callback URL & Verify Token

### Setup Webhooks in Facebook App

* Go to **Messenger → Webhooks**
* Click **Add Callback URL**

### Required Fields

* **Callback URL**: n8n webhook URL
* **Verify Token**: Any custom string (example: `my_verify_token_123`)

### Verification Logic (Important)

Facebook sends:

* `hub.mode`
* `hub.verify_token`
* `hub.challenge`

Your webhook must:

* Match the verify token
* Return `hub.challenge`

Without this, webhook will NOT be verified.

---

## 5. Train Agent Using Messages

### Message Flow

1. User sends message on Facebook Page
2. Facebook sends message data to n8n webhook
3. n8n processes the message
4. Agent (AI or logic-based) generates response
5. n8n sends reply back to Facebook Messenger

### Training Options

* Rule-based replies (keyword matching)
* AI Agent (OpenAI / Custom LLM)
* Predefined FAQ flows

### Example Training Data

* Greeting messages
* Business FAQs
* Order / Support questions

---

## Notes

* Facebook App Review may be required for advanced permissions
* Always test in **Development Mode** before going Live
* Do not expose Page Access Token publicly

---

## Tech Stack

* Facebook Developer Platform
* Facebook Messenger API
* n8n Automation Tool
* AI Agent (Optional)

---

## Status

Ready for Messenger Automation 🚀
