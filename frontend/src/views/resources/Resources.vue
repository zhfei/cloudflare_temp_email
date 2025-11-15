<script setup>
import { useI18n } from 'vue-i18n'
import { useHead } from '@unhead/vue'
import { useRouter } from 'vue-router'
import { getRouterPathWithLang } from '../../utils'
import { useIsMobile } from '../../utils/composables'

const isMobile = useIsMobile()

const router = useRouter()
const { locale, t } = useI18n({
  messages: {
    en: {
      title: 'Resources & Documentation',
      subtitle: 'Technical resources, guides, and documentation for developers',
      tutorials: 'Tutorials',
      apiDocs: 'API Documentation',
      techStack: 'Technology Stack',
      security: 'Security Guides',
      deployment: 'Deployment Guides',
      viewGuide: 'View Guide',
      viewDocs: 'View Documentation'
    },
    zh: {
      title: '资源与文档',
      subtitle: '面向开发者的技术资源、指南和文档',
      tutorials: '教程',
      apiDocs: 'API 文档',
      techStack: '技术栈',
      security: '安全指南',
      deployment: '部署指南',
      viewGuide: '查看指南',
      viewDocs: '查看文档'
    }
  }
})

useHead({
  title: t('title'),
  meta: [
    { name: 'description', content: t('subtitle') }
  ]
})

const resources = ref([
  {
    category: 'tutorials',
    title: {
      en: 'Getting Started with Cloudflare Workers',
      zh: 'Cloudflare Workers 入门指南'
    },
    description: {
      en: 'Learn the basics of Cloudflare Workers and how to build serverless applications.',
      zh: '了解 Cloudflare Workers 的基础知识以及如何构建无服务器应用。'
    },
    link: '/blog/cloudflare-workers-guide'
  },
  {
    category: 'techStack',
    title: {
      en: 'Rust WASM Email Parsing',
      zh: 'Rust WASM 邮件解析'
    },
    description: {
      en: 'Deep dive into using Rust WebAssembly for high-performance email parsing.',
      zh: '深入了解使用 Rust WebAssembly 进行高性能邮件解析。'
    },
    link: '/blog/rust-wasm-email-parsing'
  },
  {
    category: 'security',
    title: {
      en: 'Email Security: DKIM, SPF, DMARC',
      zh: '邮件安全：DKIM、SPF、DMARC'
    },
    description: {
      en: 'Comprehensive guide to email authentication protocols and security best practices.',
      zh: '邮件认证协议和安全最佳实践的全面指南。'
    },
    link: '/blog/email-security-dkim-spf'
  },
  {
    category: 'tutorials',
    title: {
      en: 'S3 Attachment Storage Setup',
      zh: 'S3 附件存储设置'
    },
    description: {
      en: 'Step-by-step guide to configuring S3-compatible storage for email attachments.',
      zh: '为邮件附件配置 S3 兼容存储的分步指南。'
    },
    link: '/blog/s3-attachment-storage'
  },
  {
    category: 'deployment',
    title: {
      en: 'SMTP/IMAP Proxy Configuration',
      zh: 'SMTP/IMAP 代理配置'
    },
    description: {
      en: 'Complete guide to setting up SMTP/IMAP proxy servers for email clients.',
      zh: '为邮件客户端设置 SMTP/IMAP 代理服务器的完整指南。'
    },
    link: '/blog/smtp-imap-proxy-setup'
  },
  {
    category: 'security',
    title: {
      en: 'Privacy Protection Guide',
      zh: '隐私保护指南'
    },
    description: {
      en: 'Learn about email tracking and how to protect your digital privacy.',
      zh: '了解邮件追踪以及如何保护您的数字隐私。'
    },
    link: '/blog/privacy-protection-guide'
  }
])

const categories = ref([
  { key: 'all', label: { en: 'All Resources', zh: '所有资源' } },
  { key: 'tutorials', label: { en: 'Tutorials', zh: '教程' } },
  { key: 'techStack', label: { en: 'Technology Stack', zh: '技术栈' } },
  { key: 'security', label: { en: 'Security', zh: '安全' } },
  { key: 'deployment', label: { en: 'Deployment', zh: '部署' } }
])

const selectedCategory = ref('all')
const filteredResources = ref(resources.value)

const filterByCategory = (category) => {
  selectedCategory.value = category
  if (category === 'all') {
    filteredResources.value = resources.value
  } else {
    filteredResources.value = resources.value.filter(resource => resource.category === category)
  }
}

const goToResource = (link) => {
  router.push(getRouterPathWithLang(link, locale.value))
}
</script>

<template>
  <div class="resources-container">
    <n-card :bordered="false">
      <div class="resources-header">
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

      <!-- 资源列表 -->
      <n-list>
        <n-list-item v-for="resource in filteredResources" :key="resource.link">
          <n-card hoverable @click="goToResource(resource.link)" style="cursor: pointer;">
            <n-space vertical>
              <div>
                <h3 style="margin: 0 0 8px 0;">{{ resource.title[locale] }}</h3>
                <n-text depth="3">{{ resource.description[locale] }}</n-text>
              </div>
              <n-space>
                <n-tag size="small" type="info">
                  {{ categories.find(c => c.key === resource.category)?.label[locale] }}
                </n-tag>
                <n-button text size="small" type="primary">
                  {{ t('viewGuide') }} →
                </n-button>
              </n-space>
            </n-space>
          </n-card>
        </n-list-item>
      </n-list>

      <!-- 技术栈信息 -->
      <n-divider />
      <h2>{{ t('techStack') }}</h2>
      <n-grid :cols="isMobile ? 1 : 2" :x-gap="16" :y-gap="16" style="margin-top: 16px;">
        <n-gi>
          <n-card title="Frontend">
            <n-list>
              <n-list-item>Vue 3 + TypeScript</n-list-item>
              <n-list-item>Vite</n-list-item>
              <n-list-item>Naive UI</n-list-item>
              <n-list-item>Rust WASM</n-list-item>
            </n-list>
          </n-card>
        </n-gi>
        <n-gi>
          <n-card title="Backend">
            <n-list>
              <n-list-item>Cloudflare Workers</n-list-item>
              <n-list-item>Hono Framework</n-list-item>
              <n-list-item>Cloudflare D1</n-list-item>
              <n-list-item>Cloudflare KV/R2</n-list-item>
            </n-list>
          </n-card>
        </n-gi>
      </n-grid>
    </n-card>
  </div>
</template>

<style scoped>
.resources-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 24px;
}

.resources-header {
  text-align: center;
  margin-bottom: 24px;
}

.resources-header h1 {
  font-size: 2.5em;
  margin-bottom: 12px;
}

.subtitle {
  font-size: 1.2em;
  color: var(--n-text-color-2);
}
</style>
