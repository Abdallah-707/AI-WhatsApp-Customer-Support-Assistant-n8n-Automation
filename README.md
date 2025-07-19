[![Support Palestine](https://raw.githubusercontent.com/Ademking/Support-Palestine/main/Support-Palestine.svg)](https://www.map.org.uk)

# 🤖 AI WhatsApp Customer-Support Assistant (n8n Automation)
![AI WhatsApp Customer-Support](https://cdn.blog.desk360.com/content/uploads/2021/08/whatsapp-business-for-customer-service-1.jpg)

This project is a **plug-and-play AI support chatbot** for WhatsApp using **n8n**, **OpenAI**, and **custom site crawlers**. It works for **any business** and answers customer queries in real time by scraping your live website content—no training needed.

---

## 🧠 What It Does

- 🟢 Automatically replies to WhatsApp messages using an AI agent
- 🧾 Crawls your website live to extract current product, pricing, policy, or support info
- 💬 Responds with short, brand-friendly messages—no hallucinations
- 🔁 Handles follow-up chats within 24 hours, or reopens conversation using a WhatsApp template
- 🗃 Maintains memory per user using PostgreSQL (e.g., Supabase)
- 🔐 Works with token-protected API for link crawling and page scraping

---

## 🔧 Technologies Used

| Feature                  | Tech / API                     |
|--------------------------|-------------------------------|
| Messaging Platform       | WhatsApp Cloud API             |
| AI Model                 | OpenAI GPT-4o-mini             |
| Memory per user          | PostgreSQL / Supabase          |
| Crawler Tools            | `list_links`, `get_page` HTTP APIs |
| Automation Engine        | [n8n.io](https://n8n.io)       |

---

## 🗂️ Flow Overview

1. **WhatsApp Trigger** receives a message from a user
2. AI Agent reads the message and uses:
   - `list_links(url)` to get internal links on your website
   - `get_page(url)` to extract clean text from selected pages
3. The AI selects and quotes factual answers based on live content
4. If no answer is found, the bot responds with:
   > “I can't find that information on our site right now. Do you want me to put you through to a human agent?”
5. If it’s been more than 24h since the last message, the bot sends a pre-approved template to reopen the chat

---

## ⚙️ How to Set It Up

### Step 1: 🔑 Activate Membership for Crawling Tools

- Get your **auth token** here: [lemolex.gumroad.com/l/ejsnx](https://lemolex.gumroad.com/l/ejsnx)
- Paste this token in the body of both `list_links` and `get_page` nodes under:
  - `auth-token`: `YOUR-TOKEN-HERE`

### Step 2: 🌐 Customize for Your Company

- Open the **AI Agent** node and:
  - Replace `[Company Name]` with your brand
  - Replace `https://www.your-company-url.com` with your website's root URL

- In `list_links` and `get_page` nodes:
  - Set `url` to your company homepage

### Step 3: 🔌 Connect Credentials

- ✅ OpenAI: Link your OpenAI account to the GPT-4o-mini node
- ✅ PostgreSQL: Connect your Supabase/Postgres DB to the `Postgres Users Memory` node
- ✅ WhatsApp: Link your WhatsApp Cloud API credentials in:
  - `WhatsApp Trigger`
  - `Send AI Agent's Answer`
  - `Send Pre-approved Template Message to Reopen the Conversation`

> 💡 Optional: Disable the 24h conversation check by removing related nodes if not needed

---

## 🗃 Data Flow & Logic

- All queries are answered using your live site — no need for manual training
- The system searches up to 8 pages deep and avoids external or dead links
- Cleaned responses are stripped of markdown formatting
- User message history is tracked via session key (user ID)

---

## 🔐 Sample Security Rules

- No off-site content is processed
- All links are filtered for safety
- Only content from your own domain is ever used

---

## 🧪 Example Responses

> “We offer free shipping on all orders over $49. You can see the full shipping policy here: Shipping Info https://your-company.com/shipping”

> “Our return window is 30 days from delivery. Full return policy: Returns https://your-company.com/returns”

---

## 🕒 24h Follow-up Flow

- WhatsApp conversations expire after 24 hours
- This system checks the last timestamp
- If expired, it sends a pre-approved template to reopen the thread

---

## 📄 License

This project is licensed under the **MIT License**.
