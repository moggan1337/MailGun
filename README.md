# MailGun 📧
## 🎬 Demo
![MailGun Demo](demo.gif)

*Email automation and delivery tracking*

## Screenshots
| Component | Preview |
|-----------|---------|
| Compose View | ![compose](screenshots/compose.png) |
| Delivery Stats | ![stats](screenshots/delivery-stats.png) |
| Webhook Log | ![webhooks](screenshots/webhooks.png) |

## Visual Description
Compose view shows email template with variable substitution. Delivery stats display open rates and click tracking. Webhook log shows incoming events with payloads.

---



> **Email Automation and Delivery API** - Send, Track, and Analyze Emails at Scale

[![npm](https://img.shields.io/npm/v/mailgun.svg)](https://www.npmjs.com/package/mailgun)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue.svg)](https://www.typescriptlang.org/)
[![Node](https://img.shields.io/badge/Node-18+-green.svg)](https://nodejs.org/)

---

## 🎯 What is MailGun?

MailGun is a powerful, developer-friendly email automation and delivery API built with TypeScript. It provides everything you need to send, track, and analyze emails at scale - from transactional emails to complex email campaigns.

### Why MailGun?

| Feature | Benefit |
|---------|---------|
| **TypeScript Native** | Full type safety and IntelliSense support |
| **Modern API** | Promise-based async/await interface |
| **Comprehensive** | From sending to analytics in one library |
| **Well Documented** | 1000+ lines of documentation |
| **Actively Maintained** | Regular updates and security patches |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                           MailGun API                                │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌──────────────┐     ┌──────────────┐     ┌──────────────────┐  │
│  │              │     │              │     │                  │  │
│  │     Send      │────▶│   Template   │────▶│     Tracking      │  │
│  │    Module     │     │    Engine    │     │      Events      │  │
│  │              │     │              │     │                  │  │
│  └──────────────┘     └──────────────┘     └────────┬─────────┘  │
│                                                        │             │
│                                                        ▼             │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │                    Webhook Dispatcher                          │  │
│  │  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐  ┌────────┐ │  │
│  │  │Delivered│  │ Opened │  │Clicked │  │Bounced │  │Complain│ │  │
│  │  └────────┘  └────────┘  └────────┘  └────────┘  └────────┘ │  │
│  └──────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │                    Analytics Engine                            │  │
│  │  ┌────────┐  ┌─────────┐  ┌────────────┐  ┌────────────┐  │  │
│  │  │ Opens  │  │  Clicks │  │Deliverability│ │   Bounces  │  │  │
│  │  └────────┘  └─────────┘  └────────────┘  └────────────┘  │  │
│  └──────────────────────────────────────────────────────────────┘  │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### Component Overview

| Component | Responsibility |
|-----------|----------------|
| **Send Module** | Constructs and dispatches emails via API |
| **Template Engine** | Renders Handlebars templates with data |
| **Tracking Service** | Records opens, clicks, and deliveries |
| **Webhook Dispatcher** | Routes incoming webhook events |
| **Analytics Engine** | Aggregates metrics and generates reports |
| **Validator** | Verifies email addresses and deliverability |

---

## ✨ Features

### Core Features

| Feature | Description |
|---------|-------------|
| **Transactional Email** | Send individual emails with rich content |
| **Batch Sending** | Send to multiple recipients efficiently |
| **Email Templates** | Reusable, data-driven email templates |
| **Tracking** | Open, click, and delivery tracking |
| **Webhooks** | Real-time event notifications |
| **Analytics** | Comprehensive email metrics |
| **Validation** | Email address verification |
| **Bounce Handling** | Automatic bounce detection and suppression |
| **Rate Limiting** | Built-in request throttling |
| **Retry Logic** | Automatic retry with exponential backoff |

### Advanced Features

| Feature | Description |
|---------|-------------|
| **Scheduled Delivery** | Send emails at specific times |
| **Tagging** | Organize and filter emails by tag |
| **Custom Headers** | Add custom MIME headers |
| **Inline Attachments** | Attach files inline for display |
| **MIME Building** | Construct complex multipart messages |
| **DKIM Signing** | Automatic email authentication |
| **SPF Validation** | Sender policy framework |

---

## 🚀 Quick Start

### Installation

```bash
# Using npm
npm install mailgun

# Using yarn
yarn add mailgun

# Using pnpm
pnpm add mailgun

# Using bun
bun add mailgun
```

### Prerequisites

1. Node.js 18 or higher
2. A MailGun account with verified domain
3. Your MailGun API key

### Basic Setup

```typescript
import { MailGun, EmailMessage } from 'mailgun';

// Initialize the client
const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'your-domain.com',
});

// Verify your credentials
const verified = await mailgun.verifyCredentials();
console.log('Credentials valid:', verified);
```

### Send Your First Email

```typescript
import { MailGun, EmailMessage } from 'mailgun';

const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'your-domain.com',
});

// Define your email
const message: EmailMessage = {
  from: 'sender@your-domain.com',
  to: ['recipient@example.com'],
  subject: 'Hello from MailGun!',
  html: `
    <h1>Welcome!</h1>
    <p>This email was sent using MailGun.</p>
  `,
  text: 'Welcome! This email was sent using MailGun.', // Plain text version
};

// Send the email
try {
  const result = await mailgun.send(message);
  console.log('✅ Email sent successfully!');
  console.log('Message ID:', result.id);
  console.log('Status:', result.status);
} catch (error) {
  console.error('❌ Failed to send:', error.message);
}
```

---

## 📖 Usage Examples

### Example 1: Simple Transactional Email

```typescript
import { MailGun } from 'mailgun';

const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
});

// Send a welcome email
async function sendWelcomeEmail(user: User): Promise<void> {
  const result = await mailgun.send({
    from: 'MyApp <noreply@myapp.com>',
    to: user.email,
    subject: `Welcome to MyApp, ${user.name}!`,
    html: `
      <h1>Welcome, ${user.name}!</h1>
      <p>Thanks for joining MyApp. We're excited to have you!</p>
      <p>Click here to verify your email: <a href="${user.verifyLink}">Verify Email</a></p>
    `,
  });
  
  console.log('Welcome email sent:', result.id);
}
```

### Example 2: Email with Attachments

```typescript
import { MailGun } from 'mailgun';

const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
});

async function sendInvoice(invoice: Invoice): Promise<void> {
  const result = await mailgun.send({
    from: 'Billing <billing@myapp.com>',
    to: invoice.customerEmail,
    subject: `Invoice #${invoice.number} from MyApp`,
    html: `
      <h1>Invoice #${invoice.number}</h1>
      <p>Total: $${invoice.total.toFixed(2)}</p>
      <p>Due: ${invoice.dueDate}</p>
    `,
    attachments: [
      {
        filename: `invoice-${invoice.number}.pdf`,
        contentType: 'application/pdf',
        data: invoice.pdfBuffer,
      },
    ],
  });
  
  console.log('Invoice sent:', result.id);
}
```

### Example 3: Using Email Templates

```typescript
import { MailGun, TemplateOptions } from 'mailgun';

const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
});

// Define template data
const templateData = {
  user: {
    name: 'John Doe',
    email: 'john@example.com',
    avatarUrl: 'https://example.com/avatars/john.jpg',
  },
  order: {
    number: 'ORD-12345',
    items: [
      { name: 'Widget Pro', quantity: 2, price: 29.99 },
      { name: 'Gadget Plus', quantity: 1, price: 49.99 },
    ],
    subtotal: 109.97,
    shipping: 9.99,
    total: 119.96,
  },
  shippingAddress: {
    line1: '123 Main St',
    city: 'San Francisco',
    state: 'CA',
    zip: '94102',
  },
};

// Send with template
const result = await mailgun.sendWithTemplate({
  from: 'MyApp <orders@myapp.com>',
  to: 'john@example.com',
  template: 'order-confirmation',
  templateData,
  subject: `Order Confirmation #${templateData.order.number}`,
});

console.log('Template email sent:', result.id);
```

### Example 4: Batch Sending

```typescript
import { MailGun, BatchMessage } from 'mailgun';

const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
});

// Create batch message
const batch: BatchMessage = {
  from: 'MyApp <notifications@myapp.com>',
  subject: 'Scheduled Maintenance Notice',
  html: `
    <h1>Scheduled Maintenance</h1>
    <p>Hi {{name}},</p>
    <p>We'll be performing scheduled maintenance on {{date}}.</p>
    <p>Duration: {{duration}}</p>
  `,
};

// Add recipients with personalization
const users = [
  { email: 'user1@example.com', name: 'Alice', date: 'Saturday', duration: '2 hours' },
  { email: 'user2@example.com', name: 'Bob', date: 'Sunday', duration: '3 hours' },
  { email: 'user3@example.com', name: 'Carol', date: 'Saturday', duration: '2 hours' },
];

for (const user of users) {
  batch.personalization = [
    { field: 'name', value: user.name },
    { field: 'date', value: user.date },
    { field: 'duration', value: user.duration },
  ];
  batch.to = [user.email];
}

// Send batch
const result = await mailgun.sendBatch(batch);
console.log(`Batch sent: ${result.sent} emails`);
```

### Example 5: Tracking Email Events

```typescript
import { MailGun } from 'mailgun';

const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
  tracking: {
    open: true,
    click: true,
    delivery: true,
  },
});

// Get events for a message
async function trackMessage(messageId: string): Promise<void> {
  const events = await mailgun.getEvents({
    messageId,
    limit: 100,
  });

  for (const event of events) {
    switch (event.event) {
      case 'accepted':
        console.log(`✓ Email accepted at ${event.timestamp}`);
        break;
      case 'delivered':
        console.log(`✓ Delivered to ${event.recipient} at ${event.timestamp}`);
        break;
      case 'opened':
        console.log(`👁 Opened by ${event.recipient} at ${event.timestamp}`);
        break;
      case 'clicked':
        console.log(`🔗 Clicked by ${event.recipient} at ${event.timestamp}`);
        console.log(`   URL: ${event.url}`);
        break;
      case 'bounced':
        console.log(`✗ Bounced: ${event.reason}`);
        break;
      case 'complained':
        console.log(`⚠️  Marked as spam by ${event.recipient}`);
        break;
      case 'unsubscribed':
        console.log(`🚫 Unsubscribed: ${event.recipient}`);
        break;
    }
  }
}
```

### Example 6: Webhook Handler

```typescript
import { WebhookHandler } from 'mailgun';
import express from 'express';

const app = express();
app.use(express.json());

const handler = new WebhookHandler({
  webhookSecret: process.env.MAILGUN_WEBHOOK_SECRET!,
});

// Register webhook endpoint
app.post('/webhooks/mailgun', async (req, res) => {
  try {
    // Verify webhook signature
    const event = await handler.verify(req);
    
    // Handle based on event type
    switch (event.event) {
      case 'delivered':
        await updateDeliveryStatus(event);
        await sendWebhookConfirmation(event);
        break;
        
      case 'opened':
        await trackEmailOpen(event);
        await updateAnalytics(event);
        break;
        
      case 'clicked':
        await trackLinkClick(event);
        await updateConversionMetrics(event);
        break;
        
      case 'bounced':
        await handleBounce(event);
        await markEmailInvalid(event);
        await alertAdmin(event);
        break;
        
      case 'complained':
        await handleSpamComplaint(event);
        await suppressEmail(event);
        break;
        
      case 'unsubscribed':
        await handleUnsubscribe(event);
        await updatePreferences(event);
        break;
    }
    
    res.status(200).send('OK');
  } catch (error) {
    console.error('Webhook error:', error);
    res.status(400).send('Invalid signature');
  }
});

app.listen(3000, () => {
  console.log('Webhook server listening on port 3000');
});
```

### Example 7: Email Validation

```typescript
import { MailGun } from 'mailgun';

const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
});

const validator = mailgun.validator;

// Validate a single email
async function validateUserEmail(email: string): Promise<boolean> {
  const result = await validator.verify(email);
  
  if (!result.isValid) {
    console.log('Invalid email reasons:', result.reasons);
    return false;
  }
  
  if (result.isDisposable) {
    console.log('Warning: Disposable email address');
    return false;
  }
  
  if (result.suggestion) {
    console.log(`Did you mean: ${result.suggestion}?`);
  }
  
  return true;
}

// Batch validate signup emails
async function validateSignups(emails: string[]): Promise<string[]> {
  const results = await validator.verifyBatch(emails);
  
  const validEmails: string[] = [];
  const invalidEmails: string[] = [];
  
  for (const result of results) {
    if (result.isValid && !result.isDisposable) {
      validEmails.push(result.address);
    } else {
      invalidEmails.push(result.address);
    }
  }
  
  console.log(`Valid: ${validEmails.length}, Invalid: ${invalidEmails.length}`);
  return validEmails;
}
```

### Example 8: Analytics Dashboard

```typescript
import { MailGun } from 'mailgun';

const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
});

const analytics = mailgun.analytics;

// Get comprehensive stats
async function getEmailStats(startDate: string, endDate: string): Promise<Stats> {
  const stats = await analytics.getStats({
    start: startDate,
    end: endDate,
    resolution: 'day',
  });
  
  return {
    total: stats.totals,
    byDay: stats.daily,
    byRecipient: stats.byRecipient,
    byTag: stats.byTag,
  };
}

// Generate report
async function generateMonthlyReport(): Promise<void> {
  const now = new Date();
  const lastMonth = new Date(now.getFullYear(), now.getMonth() - 1);
  
  const report = await analytics.getReport({
    start: lastMonth.toISOString().split('T')[0],
    end: now.toISOString().split('T')[0],
    metrics: ['sent', 'delivered', 'opened', 'clicked', 'bounced'],
    groupBy: ['day', 'campaign'],
  });
  
  // Calculate rates
  const deliveryRate = (report.delivered / report.sent * 100).toFixed(2);
  const openRate = (report.opened / report.delivered * 100).toFixed(2);
  const clickRate = (report.clicked / report.opened * 100).toFixed(2);
  
  console.log(`
    Monthly Email Report
    ====================
    Sent: ${report.sent}
    Delivered: ${report.delivered} (${deliveryRate}%)
    Opened: ${report.opened} (${openRate}%)
    Clicked: ${report.clicked} (${clickRate}%)
    Bounced: ${report.bounced}
  `);
}
```

---

## ⚙️ Configuration

### Environment Variables

| Variable | Description | Required | Example |
|----------|-------------|----------|---------|
| `MAILGUN_API_KEY` | Your MailGun API key | ✅ | `key-xxxxxxxxxxxx` |
| `MAILGUN_DOMAIN` | Your sending domain | ✅ | `mg.myapp.com` |
| `MAILGUN_WEBHOOK_SECRET` | Webhook signing secret | No | `whsec_xxxx` |
| `MAILGUN_ENDPOINT` | API endpoint | No | `api.mailgun.net` |
| `MAILGUN_REGION` | Region (us/eu) | No | `us` |

### Configuration Options

```typescript
interface MailGunConfig {
  // Required
  apiKey: string;
  domain: string;
  
  // Optional - Defaults shown
  endpoint?: string = 'api.mailgun.net';
  region?: 'us' | 'eu' = 'us';
  timeout?: number = 30000; // 30 seconds
  
  // Tracking options
  tracking?: {
    open?: boolean = true;
    click?: boolean = true;
    delivery?: boolean = true;
  };
  
  // Retry options
  retry?: {
    attempts?: number = 3;
    delay?: number = 1000; // Initial delay in ms
    maxDelay?: number = 30000; // Max delay between retries
    factor?: number = 2; // Exponential backoff factor
  };
  
  // Rate limiting
  rateLimit?: {
    maxRequests?: number = 100;
    intervalMs?: number = 60000; // Per minute
  };
  
  // Logging
  logger?: {
    enabled?: boolean = false;
    level?: 'debug' | 'info' | 'warn' | 'error' = 'info';
  };
}
```

### Example Configuration Files

**TypeScript/JavaScript:**

```typescript
import { MailGun } from 'mailgun';

const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: process.env.MAILGUN_DOMAIN!,
  timeout: 60000,
  tracking: {
    open: true,
    click: true,
    delivery: true,
  },
  retry: {
    attempts: 5,
    delay: 2000,
    factor: 2,
  },
});
```

**YAML (config.yaml):**

```yaml
mailgun:
  api_key: ${MAILGUN_API_KEY}
  domain: ${MAILGUN_DOMAIN}
  endpoint: api.mailgun.net
  region: us
  timeout: 60000
  tracking:
    open: true
    click: true
    delivery: true
  retry:
    attempts: 5
    delay: 2000
    factor: 2
```

---

## 📊 Analytics API

### Available Metrics

| Metric | Description |
|--------|-------------|
| `sent` | Total emails sent |
| `delivered` | Successfully delivered |
| `opened` | Opened by recipient |
| `clicked` | Link clicked by recipient |
| `bounced` | Bounced (hard/soft) |
| `complained` | Marked as spam |
| `unsubscribed` | Unsubscribed |

### Example Queries

```typescript
const analytics = mailgun.analytics;

// Hourly stats for a day
const hourly = await analytics.getHourlyStats({
  start: '2024-01-15T00:00:00Z',
  end: '2024-01-15T23:59:59Z',
});

// Daily stats for a month
const daily = await analytics.getDailyStats({
  start: '2024-01-01',
  end: '2024-01-31',
});

// Stats by tag
const byTag = await analytics.getStatsByTag({
  tags: ['newsletter', 'transactional', 'promotional'],
  start: '2024-01-01',
  end: '2024-01-31',
});

// Delivery timeline
const timeline = await analytics.getTimeline({
  recipient: 'user@example.com',
  limit: 50,
});
```

---

## 🔐 Security Best Practices

### 1. Protect Your API Key

```typescript
// ✅ Good - Environment variable
const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
});

// ❌ Bad - Hardcoded key
const mailgun = new MailGun({
  apiKey: 'key-1234567890abcdef',
  domain: 'myapp.com',
});
```

### 2. Verify Webhook Signatures

```typescript
const handler = new WebhookHandler({
  webhookSecret: process.env.MAILGUN_WEBHOOK_SECRET!,
  rejectInvalid: true, // Reject invalid signatures
});
```

### 3. Implement Rate Limiting

```typescript
const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
  rateLimit: {
    maxRequests: 100, // Max requests
    intervalMs: 60000, // Per minute
  },
});
```

### 4. Use TLS

```typescript
const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
  secure: true, // Force HTTPS
});
```

---

## ⚡ Performance Tips

### 1. Use Batch Sending

```typescript
// ❌ Slow - Individual requests
for (const email of emails) {
  await mailgun.send(email);
}

// ✅ Fast - Single batch request
await mailgun.sendBatch(emails);
```

### 2. Reuse Client Instance

```typescript
// Create once, use everywhere
export const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
});

// Use in multiple functions
export async function sendEmail(...) { mailgun.send(...); }
export async function sendBulk(...) { mailgun.sendBatch(...); }
```

### 3. Enable Connection Pooling

```typescript
const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
  keepAlive: true, // Reuse connections
  maxConnections: 10, // Connection pool size
});
```

### 4. Use Async/Await Properly

```typescript
// ❌ Sequential
const result1 = await sendEmail1();
const result2 = await sendEmail2();
const result3 = await sendEmail3();

// ✅ Parallel
const [result1, result2, result3] = await Promise.all([
  sendEmail1(),
  sendEmail2(),
  sendEmail3(),
]);
```

---

## 🐛 Troubleshooting

### Common Issues

#### Issue: Authentication Failed

**Symptom:** `Error: Invalid API key`

**Solution:** 
1. Verify your API key starts with `key-`
2. Check for extra whitespace in environment variable
3. Ensure you're using the correct API key (not SMTP credentials)

```typescript
// Debug
console.log('API Key prefix:', process.env.MAILGUN_API_KEY?.substring(0, 4));
```

#### Issue: Domain Not Verified

**Symptom:** `Error: Domain not found`

**Solution:**
1. Verify domain ownership in MailGun dashboard
2. Check DNS records are correctly configured
3. Wait for DNS propagation (can take up to 48 hours)

```bash
# Check DNS records
dig TXT mg.domain.com
```

#### Issue: Rate Limit Exceeded

**Symptom:** `Error: Too many requests`

**Solution:**
1. Implement exponential backoff
2. Use batch sending instead of individual sends
3. Contact MailGun to increase your limit

```typescript
const mailgun = new MailGun({
  apiKey: process.env.MAILGUN_API_KEY!,
  domain: 'myapp.com',
  retry: {
    attempts: 5,
    delay: 1000,
    factor: 2,
  },
});
```

#### Issue: Webhook Verification Failed

**Symptom:** `Error: Invalid webhook signature`

**Solution:**
1. Use the correct webhook secret (not API key)
2. Ensure raw body is being passed to verify function
3. Check timestamp is within tolerance

```typescript
// Express - ensure raw body is available
app.use('/webhooks', express.raw({ type: 'application/json' }));
app.post('/webhooks', async (req, res) => {
  const event = await handler.verify({
    body: req.body,
    signature: req.headers['mailgun-signature'],
    timestamp: req.headers['mailgun-timestamp'],
  });
});
```

#### Issue: Emails Going to Spam

**Symptom:** Low deliverability, spam complaints

**Solution:**
1. Authenticate with DKIM and SPF
2. Remove spam trigger words
3. Keep lists clean (remove bounces)
4. Warm up new domains
5. Use double opt-in

---

## 📚 API Reference

### Classes

| Class | Description |
|-------|-------------|
| `MailGun` | Main API client |
| `Validator` | Email validation |
| `WebhookHandler` | Webhook processing |
| `Analytics` | Statistics and metrics |
| `TemplateEngine` | Template rendering |

### MailGun Methods

| Method | Description |
|--------|-------------|
| `send(message)` | Send a single email |
| `sendBatch(messages)` | Send multiple emails |
| `sendWithTemplate(options)` | Send template email |
| `getEvents(filters)` | Get email events |
| `verifyCredentials()` | Verify API credentials |
| `getDomains()` | List your domains |
| `createTemplate(template)` | Create email template |
| `getTemplate(name)` | Get template by name |
| `listTemplates()` | List all templates |

### Validator Methods

| Method | Description |
|--------|-------------|
| `verify(email)` | Verify single email |
| `verifyBatch(emails)` | Verify multiple emails |
| `checkDeliverability(email)` | Check if deliverable |

### Analytics Methods

| Method | Description |
|--------|-------------|
| `getStats(options)` | Get aggregated stats |
| `getHourlyStats(options)` | Get hourly breakdown |
| `getDailyStats(options)` | Get daily breakdown |
| `getStatsByTag(options)` | Get stats by tag |
| `getTimeline(options)` | Get recipient timeline |

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

### Development Setup

```bash
# Clone repository
git clone https://github.com/moggan1337/mailgun.git
cd mailgun

# Install dependencies
npm install

# Run tests
npm test

# Build
npm run build

# Lint
npm run lint
```

### Pull Request Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Add tests
5. Ensure tests pass
6. Commit with clear messages
7. Push to your fork
8. Open a Pull Request

---

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgments

- MailGun API team for excellent documentation
- TypeScript team for amazing type system
- Node.js community for async patterns
- All contributors who improve this library

---

**Built with ❤️ by [moggan1337](https://github.com/moggan1337)**
