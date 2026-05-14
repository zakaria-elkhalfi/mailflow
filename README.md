# MailFlow — Email Automation System

A clean, production-ready email automation dashboard built with Node.js, Express, and Nodemailer.

---

## 🚀 Quick Start

### 1. Install Dependencies

```bash
cd email-automation
npm install
```

### 2. Configure Environment Variables

```bash
cp .env.example .env
```

Edit `.env` with your SMTP credentials:

```env
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_SECURE=false
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password_here
FROM_NAME=My App
PORT=3000
EMAIL_DELAY_MIN=2000
EMAIL_DELAY_MAX=5000
```

### 3. Start the Server

```bash
npm start
# or for development with auto-reload:
npm run dev
```

### 4. Open in Browser

Visit **http://localhost:3000**

---

## 📧 SMTP Configuration

### Gmail (Recommended)

1. Enable **2-Step Verification** on your Google account
2. Go to: Google Account → Security → **App Passwords**
3. Create a new App Password (select "Mail")
4. Use that 16-character password as `SMTP_PASS` (NOT your Gmail password)

```env
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_SECURE=false
SMTP_USER=yourname@gmail.com
SMTP_PASS=abcd efgh ijkl mnop
```

### Outlook / Hotmail

```env
SMTP_HOST=smtp-mail.outlook.com
SMTP_PORT=587
SMTP_SECURE=false
SMTP_USER=yourname@outlook.com
SMTP_PASS=your_password
```

### Custom SMTP (e.g. Mailgun, SendGrid)

```env
SMTP_HOST=smtp.mailgun.org
SMTP_PORT=587
SMTP_USER=postmaster@your-domain.com
SMTP_PASS=your_mailgun_smtp_password
```

---

## 🎯 Features

- **Template Editor** — Save subject + message, edit anytime
- **Bulk Recipients** — Paste emails or upload a CSV file
- **Sequential Sending** — Emails sent one-by-one with random delay (2–5s default)
- **Live Progress Bar** — Real-time updates via Server-Sent Events
- **Send Log** — Full history with sent/failed status per email
- **Email Validation** — Invalid addresses are caught before sending
- **SMTP Health Check** — Test your connection from the header

---

## 📁 Project Structure

```
email-automation/
├── src/
│   └── server.js        # Express backend + all API routes
├── public/
│   └── index.html       # Frontend dashboard (single file)
├── .env.example         # Environment variable template
├── .env                 # Your credentials (NEVER commit this)
├── package.json
└── README.md
```

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/template` | Get saved template |
| POST | `/api/template` | Save template |
| POST | `/api/parse-csv` | Parse uploaded CSV |
| POST | `/api/send` | Start sending emails |
| GET | `/api/logs` | Get send history |
| DELETE | `/api/logs` | Clear logs |
| GET | `/api/test-smtp` | Test SMTP connection |
| GET | `/api/events` | SSE stream for live updates |

---

## ⚠️ Security Notes

- **Never commit `.env`** — it's already in `.gitignore`
- Credentials are only used server-side via Nodemailer
- Frontend never sees your SMTP password
- For production, add rate limiting and authentication

---

## 🛠 Troubleshooting

**"SMTP · error" in header?**
- Check your `.env` credentials
- For Gmail: make sure you're using an App Password, not your actual password
- Try toggling `SMTP_SECURE=true` with `SMTP_PORT=465`

**Emails not arriving?**
- Check spam folder
- Verify sender domain isn't blacklisted
- Lower the send rate (increase delay values)

**CSV not parsing?**
- Ensure emails are in the first column
- Try saving as plain `.csv` (not `.xlsx`)
