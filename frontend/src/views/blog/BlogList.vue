<script setup>
import { ref, onMounted } from 'vue'
import { useI18n } from 'vue-i18n'
import { useRouter } from 'vue-router'
import { getRouterPathWithLang } from '../../utils'
import { useIsMobile } from '../../utils/composables'

const isMobile = useIsMobile()

const router = useRouter()
const { locale, t } = useI18n({
  messages: {
    en: {
      title: 'Technical Blog & Resources',
      subtitle: 'Learn about Cloudflare Workers, D1, Rust WASM, and email security',
      latestArticles: 'Latest Articles',
      tutorials: 'Tutorials',
      techStack: 'Technology Stack',
      security: 'Security & Privacy',
      allArticles: 'All Articles',
      readMore: 'Read More',
      publishedOn: 'Published on'
    },
    zh: {
      title: '技术博客与资源',
      subtitle: '了解 Cloudflare Workers、D1、Rust WASM 和邮件安全',
      latestArticles: '最新文章',
      tutorials: '教程',
      techStack: '技术栈',
      security: '安全与隐私',
      allArticles: '所有文章',
      readMore: '阅读更多',
      publishedOn: '发布于'
    }
  }
})

// 博客文章列表（后续可以从 API 或静态文件加载）
const articles = ref([
  {
    id: 'cloudflare-workers-guide',
    title: {
      en: 'Building High-Performance Email Services with Cloudflare Workers',
      zh: '使用 Cloudflare Workers 构建高性能邮件服务'
    },
    excerpt: {
      en: 'Learn how to leverage Cloudflare Workers, D1 database, and KV storage to build a scalable temporary email service with zero server costs.',
      zh: '了解如何利用 Cloudflare Workers、D1 数据库和 KV 存储构建可扩展的临时邮件服务，实现零服务器成本。'
    },
    category: 'techStack',
    date: '2024-01-15',
    readTime: '8 min',
    tags: ['Cloudflare Workers', 'D1', 'Serverless']
  },
  {
    id: 'rust-wasm-email-parsing',
    title: {
      en: 'Rust WASM for Email Parsing: Performance and Reliability',
      zh: 'Rust WASM 邮件解析：性能与可靠性'
    },
    excerpt: {
      en: 'Discover why Rust WebAssembly outperforms Node.js libraries for email parsing, with detailed benchmarks and implementation guides.',
      zh: '了解为什么 Rust WebAssembly 在邮件解析方面优于 Node.js 库，包含详细的基准测试和实施指南。'
    },
    category: 'techStack',
    date: '2024-01-20',
    readTime: '10 min',
    tags: ['Rust', 'WASM', 'Performance']
  },
  {
    id: 's3-attachment-storage',
    title: {
      en: 'Secure S3 Attachment Storage Configuration Guide',
      zh: '安全的 S3 附件存储配置指南'
    },
    excerpt: {
      en: 'Complete guide to configuring S3-compatible storage for email attachments, including security best practices and cost optimization.',
      zh: '配置 S3 兼容存储用于邮件附件的完整指南，包括安全最佳实践和成本优化。'
    },
    category: 'tutorials',
    date: '2024-01-25',
    readTime: '12 min',
    tags: ['S3', 'Storage', 'Security']
  },
  {
    id: 'email-security-dkim-spf',
    title: {
      en: 'Understanding Email Security: DKIM, SPF, and DMARC Explained',
      zh: '理解邮件安全：DKIM、SPF 和 DMARC 详解'
    },
    excerpt: {
      en: 'Comprehensive guide to email authentication protocols, how they prevent spam and phishing, and how to implement them correctly.',
      zh: '邮件认证协议的全面指南，了解它们如何防止垃圾邮件和钓鱼攻击，以及如何正确实施。'
    },
    category: 'security',
    date: '2024-02-01',
    readTime: '15 min',
    tags: ['DKIM', 'SPF', 'DMARC', 'Security']
  },
  {
    id: 'smtp-imap-proxy-setup',
    title: {
      en: 'SMTP/IMAP Proxy Server Setup: Complete Configuration Tutorial',
      zh: 'SMTP/IMAP 代理服务器设置：完整配置教程'
    },
    excerpt: {
      en: 'Step-by-step guide to setting up a Python-based SMTP/IMAP proxy server for temporary email services, including Docker deployment.',
      zh: '为临时邮件服务设置基于 Python 的 SMTP/IMAP 代理服务器的分步指南，包括 Docker 部署。'
    },
    category: 'tutorials',
    date: '2024-02-05',
    readTime: '14 min',
    tags: ['SMTP', 'IMAP', 'Python', 'Docker']
  },
  {
    id: 'privacy-protection-guide',
    title: {
      en: 'Privacy Protection in the Digital Age: Email Tracking and Prevention',
      zh: '数字时代的隐私保护：邮件追踪与防护'
    },
    excerpt: {
      en: 'Learn how email tracking works, why it matters for your privacy, and how temporary email services can help protect your digital identity.',
      zh: '了解邮件追踪的工作原理，为什么它对您的隐私很重要，以及临时邮件服务如何帮助保护您的数字身份。'
    },
    category: 'security',
    date: '2024-02-10',
    readTime: '11 min',
    tags: ['Privacy', 'Email Tracking', 'Security']
  }
])

const categories = ref([
  { key: 'all', label: { en: 'All Articles', zh: '所有文章' } },
  { key: 'techStack', label: { en: 'Technology Stack', zh: '技术栈' } },
  { key: 'tutorials', label: { en: 'Tutorials', zh: '教程' } },
  { key: 'security', label: { en: 'Security & Privacy', zh: '安全与隐私' } }
])

const selectedCategory = ref('all')
const filteredArticles = ref(articles.value)

const filterByCategory = (category) => {
  selectedCategory.value = category
  if (category === 'all') {
    filteredArticles.value = articles.value
  } else {
    filteredArticles.value = articles.value.filter(article => article.category === category)
  }
}

const goToArticle = (articleId) => {
  router.push(getRouterPathWithLang(`/blog/${articleId}`, locale.value))
}

onMounted(() => {
  filterByCategory('all')
})
</script>

<template>
  <div class="blog-container">
    <n-card :bordered="false">
      <div class="blog-header">
        <h1>{{ t('title') }}</h1>
        <p class="subtitle">{{ t('subtitle') }}</p>
      </div>

      <n-divider />

      <!-- 分类导航 -->
      <n-space style="margin-bottom: 24px;" wrap>
        <n-button
          v-for="cat in categories"
          :key="cat.key"
          :type="selectedCategory === cat.key ? 'primary' : 'default'"
          @click="filterByCategory(cat.key)"
        >
          {{ cat.label[locale] }}
        </n-button>
      </n-space>

      <!-- 文章列表 -->
      <n-grid :cols="isMobile ? 1 : 3" :x-gap="16" :y-gap="16">
        <n-gi v-for="article in filteredArticles" :key="article.id">
          <n-card
            hoverable
            :title="article.title[locale]"
            style="height: 100%; cursor: pointer;"
            @click="goToArticle(article.id)"
          >
            <template #header-extra>
              <n-tag size="small" type="info">{{ article.readTime }}</n-tag>
            </template>
            
            <p style="color: var(--n-text-color-2); margin-bottom: 12px;">
              {{ article.excerpt[locale] }}
            </p>
            
            <n-space style="margin-top: 12px;" wrap>
              <n-tag
                v-for="tag in article.tags"
                :key="tag"
                size="small"
                type="default"
              >
                {{ tag }}
              </n-tag>
            </n-space>
            
            <template #footer>
              <n-text depth="3" style="font-size: 12px;">
                {{ t('publishedOn') }} {{ article.date }}
              </n-text>
            </template>
          </n-card>
        </n-gi>
      </n-grid>
    </n-card>
  </div>
</template>

<style scoped>
.blog-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 24px;
}

.blog-header {
  text-align: center;
  margin-bottom: 24px;
}

.blog-header h1 {
  font-size: 2.5em;
  margin-bottom: 12px;
}

.subtitle {
  font-size: 1.2em;
  color: var(--n-text-color-2);
}
</style>
