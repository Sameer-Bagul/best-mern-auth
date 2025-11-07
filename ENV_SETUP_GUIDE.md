# Environment Variables Setup Guide

## Required Environment Variables

This MERN auth template requires the following environment variables to be configured in the `server/.env` file:

### 1. Server Configuration

```env
PORT=3000
NODE_ENV=development  # Use 'production' for production deployment
```

### 2. MongoDB Configuration

**For Local MongoDB:**
```env
MONGODB_URI=mongodb://localhost:27017
```

**For MongoDB Atlas (Cloud):**
1. Sign up at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a cluster
3. Get your connection string
4. Replace with your credentials:
```env
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net
```

### 3. JWT Secret Key

Generate a secure random string for JWT token signing:

**Option 1 - Using Node.js:**
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

**Option 2 - Using OpenSSL:**
```bash
openssl rand -hex 32
```

Then add to `.env`:
```env
JWT_SECRET=your_generated_secret_key_here
```

### 4. Email Configuration (SMTP)

This template uses **Brevo (formerly Sendinblue)** for sending emails:

1. Sign up at [Brevo](https://www.brevo.com/)
2. Go to **SMTP & API** section
3. Get your SMTP credentials
4. Add to `.env`:

```env
SMTP_USER=your_brevo_smtp_login
SMTP_PASS=your_brevo_smtp_master_password
SENDER_EMAIL=your_verified_sender_email@example.com
```

**Alternative SMTP Providers:**
- **Gmail**: Requires App Password (not regular password)
- **SendGrid**: Popular alternative
- **Mailgun**: Another reliable option

### 5. Client URL

For CORS configuration:
```env
CLIENT_URL=http://localhost:5173
```

In production, change to your frontend domain:
```env
CLIENT_URL=https://yourdomain.com
```

## Setup Instructions

1. **Copy the example file:**
   ```bash
   cd server
   cp .env.example .env
   ```

2. **Edit `.env` file with your actual values:**
   ```bash
   nano .env  # or use your preferred editor
   ```

3. **Never commit `.env` to version control!**
   - The `.env` file is already in `.gitignore`
   - Only commit `.env.example` as a template

## Quick Setup Checklist

- [ ] MongoDB database set up (local or Atlas)
- [ ] JWT secret key generated
- [ ] Brevo account created and SMTP credentials obtained
- [ ] All environment variables added to `.env`
- [ ] `.env` file not committed to git
- [ ] Test the application

## Testing Your Setup

Start the server:
```bash
cd server
npm install
npm run dev
```

You should see:
```
Server is running on port: 3000
MongoDB connected
```

## Troubleshooting

### MongoDB Connection Error
- Check if MongoDB is running locally: `mongosh` or `mongo`
- Verify MongoDB URI is correct
- For Atlas: Check whitelist IP addresses

### Email Not Sending
- Verify SMTP credentials are correct
- Check sender email is verified in Brevo
- Look for error messages in server logs

### JWT Errors
- Ensure JWT_SECRET is set and not empty
- Make sure it's a long, random string (at least 32 characters)

## Production Deployment

When deploying to production:

1. Set `NODE_ENV=production`
2. Use strong, unique JWT_SECRET
3. Use MongoDB Atlas or managed MongoDB
4. Configure production domain in CLIENT_URL
5. Enable HTTPS
6. Never expose `.env` file

## Security Best Practices

- ✅ Use strong, unique passwords
- ✅ Never commit `.env` to version control
- ✅ Rotate JWT secrets periodically
- ✅ Use environment-specific configurations
- ✅ Enable HTTPS in production
- ✅ Keep dependencies updated
