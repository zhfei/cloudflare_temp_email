<template>
  <div class="tutorials-page">
    <n-card>
      <template #header>
        <h1>{{ t('tutorials') }}</h1>
        <n-text depth="3">{{ t('tutorialsSubtitle') }}</n-text>
      </template>

      <n-space vertical size="large">
        <n-collapse accordion>
          <n-collapse-item 
            v-for="tutorial in tutorials" 
            :key="tutorial.id"
            :name="tutorial.id"
            :title="tutorial.title"
          >
            <div class="tutorial-content" v-html="tutorial.content"></div>
          </n-collapse-item>
        </n-collapse>
      </n-space>
    </n-card>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n({
  messages: {
    en: {
      tutorials: 'Tutorials',
      tutorialsSubtitle: 'Step-by-step guides to help you get the most out of our service'
    },
    zh: {
      tutorials: '教程',
      tutorialsSubtitle: '分步指南，帮助您充分利用我们的服务'
    }
  }
})

const tutorials = ref([
  {
    id: 'getting-started',
    title: 'Getting Started: Creating Your First Temporary Email',
    content: `
      <h3>Step 1: Access the Service</h3>
      <p>Navigate to the homepage and you'll see an address bar where you can create a new temporary email address.</p>
      
      <h3>Step 2: Generate an Address</h3>
      <p>Click the "Generate" button to create a random email address, or enter a custom name for your address.</p>
      
      <h3>Step 3: Receive Emails</h3>
      <p>Use your temporary email address to sign up for services or receive verification emails. All incoming emails will appear in your inbox automatically.</p>
      
      <h3>Step 4: Manage Your Emails</h3>
      <p>You can view, reply to, forward, or delete emails directly from the web interface. Attachments are automatically processed and can be downloaded.</p>
    `
  },
  {
    id: 's3-attachment-setup',
    title: 'Configuring S3 Attachment Storage',
    content: `
      <h3>Prerequisites</h3>
      <ul>
        <li>AWS S3 bucket or Cloudflare R2 bucket</li>
        <li>Access keys with appropriate permissions</li>
        <li>Worker configuration access</li>
      </ul>
      
      <h3>Configuration Steps</h3>
      <ol>
        <li>Create an S3 bucket or R2 bucket in your cloud provider</li>
        <li>Generate access keys with read/write permissions</li>
        <li>Configure the following environment variables in your Worker:
          <ul>
            <li><code>S3_ACCESS_KEY_ID</code></li>
            <li><code>S3_SECRET_ACCESS_KEY</code></li>
            <li><code>S3_BUCKET_NAME</code></li>
            <li><code>S3_REGION</code> (for AWS S3)</li>
            <li><code>S3_ENDPOINT</code> (for R2 or custom S3-compatible storage)</li>
          </ul>
        </li>
        <li>Deploy your Worker with the new configuration</li>
        <li>Test attachment uploads and downloads</li>
      </ol>
      
      <h3>Security Best Practices</h3>
      <ul>
        <li>Use presigned URLs for temporary access</li>
        <li>Set appropriate expiration times</li>
        <li>Implement bucket policies to restrict access</li>
        <li>Enable versioning for important attachments</li>
      </ul>
    `
  },
  {
    id: 'webhook-setup',
    title: 'Setting Up Webhooks for Email Notifications',
    content: `
      <h3>What are Webhooks?</h3>
      <p>Webhooks allow you to receive real-time notifications when emails arrive at your temporary addresses. This is useful for automation and integration with other services.</p>
      
      <h3>Configuration Steps</h3>
      <ol>
        <li>Navigate to the Webhook Settings page</li>
        <li>Click "Add Webhook"</li>
        <li>Enter your webhook URL (must be HTTPS)</li>
        <li>Configure filters (optional):
          <ul>
            <li>Email address filters</li>
            <li>Keyword filters</li>
            <li>Sender filters</li>
          </ul>
        </li>
        <li>Test your webhook with a test email</li>
      </ol>
      
      <h3>Webhook Payload Format</h3>
      <pre><code>{
  "event": "email.received",
  "address": "example@domain.com",
  "from": "sender@example.com",
  "subject": "Email Subject",
  "body": "Email body text",
  "timestamp": "2025-01-27T10:00:00Z"
}</code></pre>
      
      <h3>Integration Examples</h3>
      <ul>
        <li><strong>Telegram Bot:</strong> Send notifications to a Telegram chat</li>
        <li><strong>Slack:</strong> Post messages to a Slack channel</li>
        <li><strong>Custom API:</strong> Integrate with your own backend service</li>
      </ul>
    `
  },
  {
    id: 'smtp-imap-config',
    title: 'Configuring SMTP/IMAP Proxy Server',
    content: `
      <h3>Overview</h3>
      <p>Our SMTP/IMAP proxy server allows you to use standard email clients (like Outlook, Thunderbird, or Apple Mail) with our temporary email service.</p>
      
      <h3>Docker Deployment</h3>
      <pre><code>docker run -d \\
  -p 25:25 -p 587:587 -p 993:993 \\
  -e WORKER_API_URL=https://your-worker.workers.dev \\
  -e WORKER_API_KEY=your-api-key \\
  your-image-name</code></pre>
      
      <h3>Email Client Configuration</h3>
      <h4>SMTP Settings (for sending):</h4>
      <ul>
        <li>Server: your-proxy-server.com</li>
        <li>Port: 587 (TLS) or 25</li>
        <li>Encryption: STARTTLS</li>
        <li>Authentication: Required</li>
      </ul>
      
      <h4>IMAP Settings (for receiving):</h4>
      <ul>
        <li>Server: your-proxy-server.com</li>
        <li>Port: 993</li>
        <li>Encryption: SSL/TLS</li>
        <li>Authentication: Required</li>
      </ul>
      
      <h3>Security Considerations</h3>
      <ul>
        <li>Always use TLS/SSL encryption</li>
        <li>Keep your API keys secure</li>
        <li>Monitor server logs for suspicious activity</li>
        <li>Use firewall rules to restrict access</li>
      </ul>
    `
  },
  {
    id: 'telegram-bot',
    title: 'Using Telegram Bot for Email Management',
    content: `
      <h3>Setting Up the Bot</h3>
      <ol>
        <li>Create a bot with @BotFather on Telegram</li>
        <li>Get your bot token</li>
        <li>Configure the bot token in Worker settings:
          <ul>
            <li><code>TG_BOT_TOKEN</code></li>
            <li><code>TG_WEBHOOK_URL</code></li>
          </ul>
        </li>
        <li>Set up the webhook URL for Telegram</li>
      </ol>
      
      <h3>Available Commands</h3>
      <ul>
        <li><code>/start</code> - Start using the bot</li>
        <li><code>/new</code> - Create a new temporary email address</li>
        <li><code>/list</code> - List all your email addresses</li>
        <li><code>/delete &lt;address&gt;</code> - Delete an address</li>
        <li><code>/help</code> - Show help message</li>
      </ul>
      
      <h3>Features</h3>
      <ul>
        <li>Receive email notifications in Telegram</li>
        <li>View email content directly in Telegram</li>
        <li>Manage multiple email addresses</li>
        <li>Quick access to attachments</li>
      </ul>
    `
  },
  {
    id: 'security-privacy',
    title: 'Security and Privacy Best Practices',
    content: `
      <h3>Understanding Temporary Email Security</h3>
      <p>Temporary email services provide privacy by using disposable addresses, but it's important to understand the security implications.</p>
      
      <h3>Best Practices</h3>
      <ul>
        <li><strong>Use for Non-Critical Services:</strong> Only use temporary emails for services that don't require long-term access</li>
        <li><strong>Don't Share Sensitive Information:</strong> Avoid using temporary emails for banking, healthcare, or other sensitive services</li>
        <li><strong>Regular Cleanup:</strong> Delete old emails and addresses regularly</li>
        <li><strong>Monitor Activity:</strong> Check your inbox regularly for unexpected emails</li>
      </ul>
      
      <h3>Email Tracking Protection</h3>
      <p>Our service includes features to help protect against email tracking:</p>
      <ul>
        <li>Automatic image proxy (prevents pixel tracking)</li>
        <li>Link sanitization</li>
        <li>SPF/DKIM/DMARC verification</li>
        <li>Spam detection and filtering</li>
      </ul>
      
      <h3>Data Retention</h3>
      <p>Emails are automatically deleted after a configurable retention period. You can also manually delete emails at any time. We do not store emails longer than necessary.</p>
      
      <h3>Privacy Considerations</h3>
      <ul>
        <li>We don't sell your email data</li>
        <li>Emails are encrypted in transit</li>
        <li>Access logs are minimal and anonymized</li>
        <li>You can request data deletion at any time</li>
      </ul>
    `
  }
])
</script>

<style scoped>
.tutorials-page {
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
}

.tutorial-content {
  line-height: 1.8;
  padding: 10px 0;
}

.tutorial-content h3 {
  margin-top: 20px;
  margin-bottom: 10px;
  font-size: 18px;
}

.tutorial-content h4 {
  margin-top: 15px;
  margin-bottom: 8px;
  font-size: 16px;
}

.tutorial-content ul,
.tutorial-content ol {
  padding-left: 20px;
  margin-bottom: 15px;
}

.tutorial-content li {
  margin-bottom: 8px;
}

.tutorial-content code {
  background-color: var(--n-code-color);
  padding: 2px 6px;
  border-radius: 3px;
  font-family: monospace;
}

.tutorial-content pre {
  background-color: var(--n-code-color);
  padding: 15px;
  border-radius: 5px;
  overflow-x: auto;
  margin: 15px 0;
}

.tutorial-content pre code {
  background: none;
  padding: 0;
}
</style>
