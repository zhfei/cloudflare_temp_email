<template>
  <div class="blog-page">
    <n-card>
      <template #header>
        <h1>{{ t('technicalBlog') }}</h1>
        <n-text depth="3">{{ t('blogSubtitle') }}</n-text>
      </template>

      <n-space vertical size="large">
        <article v-for="article in articles" :key="article.id" class="blog-article">
          <n-card>
            <template #header>
              <h2>{{ article.title }}</h2>
              <n-text depth="3">{{ t('published') }}: {{ article.date }}</n-text>
            </template>
            
            <div class="article-content" v-html="article.summary"></div>
            
            <template #action>
              <n-button @click="viewArticle(article.id)" type="primary">
                {{ t('readMore') }}
              </n-button>
            </template>
          </n-card>
        </article>
      </n-space>
    </n-card>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useI18n } from 'vue-i18n'
import { getRouterPathWithLang } from '../../utils'

const router = useRouter()
const { locale } = useI18n()

const { t } = useI18n({
  messages: {
    en: {
      technicalBlog: 'Technical Blog',
      blogSubtitle: 'In-depth articles about our technology stack and implementation',
      published: 'Published',
      readMore: 'Read More'
    },
    zh: {
      technicalBlog: '技术博客',
      blogSubtitle: '关于我们的技术栈和实现的深度文章',
      published: '发布时间',
      readMore: '阅读更多'
    }
  }
})

const articles = ref([
  {
    id: 'cloudflare-workers-architecture',
    title: 'Building High-Performance Email Services with Cloudflare Workers',
    date: '2025-01-20',
    summary: `
      <p>Cloudflare Workers provides a powerful edge computing platform that enables us to deliver email services with global low latency. In this article, we explore how we leverage Workers to build a scalable temporary email service.</p>
      <h3>Key Benefits:</h3>
      <ul>
        <li>Global edge network for sub-50ms response times</li>
        <li>Serverless architecture eliminates infrastructure management</li>
        <li>Built-in DDoS protection and security features</li>
        <li>Cost-effective scaling with pay-per-use pricing</li>
      </ul>
    `
  },
  {
    id: 'rust-wasm-email-parsing',
    title: 'Rust WASM: Revolutionizing Email Parsing Performance',
    date: '2025-01-18',
    summary: `
      <p>We've replaced traditional JavaScript email parsing libraries with a Rust-based WebAssembly solution, achieving significant performance improvements and better compatibility with complex email formats.</p>
      <h3>Performance Improvements:</h3>
      <ul>
        <li>3-5x faster parsing compared to Node.js libraries</li>
        <li>Better handling of RFC-compliant email formats</li>
        <li>Improved attachment processing and image rendering</li>
        <li>Reduced memory footprint</li>
      </ul>
    `
  },
  {
    id: 'cloudflare-d1-database',
    title: 'Using Cloudflare D1 for Reliable Email Storage',
    date: '2025-01-15',
    summary: `
      <p>Cloudflare D1 provides a SQLite-based database solution that integrates seamlessly with Workers. Learn how we use D1 to store emails, user data, and system configurations efficiently.</p>
      <h3>Features:</h3>
      <ul>
        <li>SQLite compatibility for familiar SQL queries</li>
        <li>Automatic replication and backup</li>
        <li>Low-latency access from Workers</li>
        <li>Cost-effective storage pricing</li>
      </ul>
    `
  },
  {
    id: 'smtp-imap-proxy-configuration',
    title: 'SMTP/IMAP Proxy Server: Complete Configuration Guide',
    date: '2025-01-12',
    summary: `
      <p>Our Python-based SMTP/IMAP proxy server enables standard email clients to work with our temporary email service. This comprehensive guide covers setup, configuration, and security best practices.</p>
      <h3>Topics Covered:</h3>
      <ul>
        <li>Docker deployment and configuration</li>
        <li>Security considerations and TLS setup</li>
        <li>Integration with Cloudflare Workers API</li>
        <li>Troubleshooting common issues</li>
      </ul>
    `
  },
  {
    id: 's3-attachment-storage',
    title: 'Secure S3 Attachment Storage: Implementation and Best Practices',
    date: '2025-01-10',
    summary: `
      <p>Learn how we implement secure attachment storage using AWS S3 and Cloudflare R2, including presigned URLs, access control, and automatic cleanup policies.</p>
      <h3>Security Features:</h3>
      <ul>
        <li>Presigned URL generation for secure access</li>
        <li>Automatic expiration and cleanup</li>
        <li>Access control and permission management</li>
        <li>Cost optimization strategies</li>
      </ul>
    `
  },
  {
    id: 'webhook-integration',
    title: 'Webhook Integration: Real-time Email Notifications',
    date: '2025-01-08',
    summary: `
      <p>Our webhook system allows you to receive real-time notifications when emails arrive. This article explains how to configure webhooks, handle retries, and integrate with popular services.</p>
      <h3>Integration Examples:</h3>
      <ul>
        <li>Telegram Bot notifications</li>
        <li>Slack integration</li>
        <li>Custom HTTP endpoints</li>
        <li>Error handling and retry logic</li>
      </ul>
    `
  }
])

const viewArticle = (articleId) => {
  router.push(getRouterPathWithLang(`/blog/${articleId}`, locale.value))
}
</script>

<style scoped>
.blog-page {
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
}

.blog-article {
  margin-bottom: 20px;
}

.blog-article h2 {
  margin: 0 0 10px 0;
  font-size: 22px;
}

.article-content {
  line-height: 1.8;
}

.article-content h3 {
  margin-top: 15px;
  margin-bottom: 10px;
  font-size: 18px;
}

.article-content ul {
  padding-left: 20px;
}

.article-content li {
  margin-bottom: 8px;
}
</style>
