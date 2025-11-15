<script setup>
import { ref, onMounted, computed } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { useI18n } from 'vue-i18n'
import { useHead } from '@unhead/vue'
import { getRouterPathWithLang } from '../../utils'

const route = useRoute()
const router = useRouter()
const { locale, t } = useI18n({
  messages: {
    en: {
      backToBlog: 'Back to Blog',
      publishedOn: 'Published on',
      readTime: 'min read',
      relatedArticles: 'Related Articles',
      tableOfContents: 'Table of Contents'
    },
    zh: {
      backToBlog: '返回博客',
      publishedOn: '发布于',
      readTime: '分钟阅读',
      relatedArticles: '相关文章',
      tableOfContents: '目录'
    }
  }
})

// 文章内容（实际应该从 API 或静态文件加载）
const articleContent = ref(null)
const article = ref(null)

// 模拟文章内容加载
const loadArticle = async () => {
  const articleId = route.params.id
  
  // 这里应该从 API 或静态文件加载实际内容
  // 为了演示，我们使用占位内容
  const articles = {
    'cloudflare-workers-guide': {
      title: {
        en: 'Building High-Performance Email Services with Cloudflare Workers',
        zh: '使用 Cloudflare Workers 构建高性能邮件服务'
      },
      content: {
        en: `
# Building High-Performance Email Services with Cloudflare Workers

Cloudflare Workers provides a powerful serverless platform for building edge applications. In this comprehensive guide, we'll explore how to leverage Cloudflare Workers, D1 database, and KV storage to build a scalable temporary email service with zero server costs.

## Introduction

Traditional email services require dedicated servers, complex infrastructure, and ongoing maintenance. Cloudflare Workers changes this paradigm by allowing you to run code at the edge, closer to your users, with automatic scaling and global distribution.

## Architecture Overview

Our email service architecture consists of:

- **Cloudflare Workers**: Handles HTTP requests and email processing
- **Cloudflare D1**: SQLite database for storing emails and user data
- **Cloudflare KV**: Key-value store for caching and temporary data
- **Cloudflare R2**: Object storage for email attachments
- **Cloudflare Email Routing**: Receives incoming emails

## Key Benefits

1. **Zero Infrastructure Costs**: Cloudflare's free tier provides generous limits
2. **Global Performance**: Edge computing ensures low latency worldwide
3. **Automatic Scaling**: No need to manage server capacity
4. **Built-in Security**: DDoS protection and SSL/TLS included

## Implementation Details

[Detailed technical content would go here...]

## Conclusion

Cloudflare Workers enables developers to build powerful email services without managing infrastructure. The combination of Workers, D1, and KV provides a complete solution for modern serverless applications.
        `,
        zh: `
# 使用 Cloudflare Workers 构建高性能邮件服务

Cloudflare Workers 提供了一个强大的无服务器平台来构建边缘应用。在本综合指南中，我们将探索如何利用 Cloudflare Workers、D1 数据库和 KV 存储构建可扩展的临时邮件服务，实现零服务器成本。

## 简介

传统的邮件服务需要专用服务器、复杂的基础设施和持续维护。Cloudflare Workers 通过允许您在边缘运行代码，更接近用户，具有自动扩展和全球分发，改变了这一范式。

## 架构概述

我们的邮件服务架构包括：

- **Cloudflare Workers**: 处理 HTTP 请求和邮件处理
- **Cloudflare D1**: SQLite 数据库用于存储邮件和用户数据
- **Cloudflare KV**: 键值存储用于缓存和临时数据
- **Cloudflare R2**: 对象存储用于邮件附件
- **Cloudflare Email Routing**: 接收传入邮件

## 主要优势

1. **零基础设施成本**: Cloudflare 免费层提供慷慨的限制
2. **全球性能**: 边缘计算确保全球低延迟
3. **自动扩展**: 无需管理服务器容量
4. **内置安全**: 包含 DDoS 保护和 SSL/TLS

## 实施细节

[详细的技术内容将在这里...]

## 结论

Cloudflare Workers 使开发人员能够构建强大的邮件服务，而无需管理基础设施。Workers、D1 和 KV 的组合为现代无服务器应用提供了完整的解决方案。
        `
      },
      date: '2024-01-15',
      readTime: 8,
      category: 'techStack',
      tags: ['Cloudflare Workers', 'D1', 'Serverless']
    }
    // 添加更多文章...
  }
  
  article.value = articles[articleId] || null
  articleContent.value = article.value?.content[locale.value] || ''
  
  if (article.value) {
    useHead({
      title: article.value.title[locale.value],
      meta: [
        { name: 'description', content: article.value.content[locale.value].substring(0, 160) },
        { property: 'og:title', content: article.value.title[locale.value] },
        { property: 'og:type', content: 'article' },
        { property: 'article:published_time', content: article.value.date }
      ]
    })
  }
}

const relatedArticles = computed(() => {
  // 返回相关文章（简化版）
  return []
})

onMounted(() => {
  loadArticle()
})
</script>

<template>
  <div class="blog-post-container">
    <n-card v-if="article" :bordered="false">
      <template #header>
        <n-space vertical>
          <n-button text @click="router.push(getRouterPathWithLang('/blog', locale))">
            <template #icon>
              <n-icon><svg viewBox="0 0 24 24"><path d="M20 11H7.83l5.59-5.59L12 4l-8 8 8 8 1.41-1.41L7.83 13H20v-2z" fill="currentColor"/></svg></n-icon>
            </template>
            {{ t('backToBlog') }}
          </n-button>
          
          <h1>{{ article.title[locale] }}</h1>
          
          <n-space>
            <n-text depth="3">{{ t('publishedOn') }} {{ article.date }}</n-text>
            <n-divider vertical />
            <n-text depth="3">{{ article.readTime }} {{ t('readTime') }}</n-text>
            <n-divider vertical />
            <n-tag
              v-for="tag in article.tags"
              :key="tag"
              size="small"
              type="info"
            >
              {{ tag }}
            </n-tag>
          </n-space>
        </n-space>
      </template>

      <div class="article-content" v-html="articleContent"></div>

      <template #footer>
        <n-divider />
        <h3>{{ t('relatedArticles') }}</h3>
        <p v-if="relatedArticles.length === 0" style="color: var(--n-text-color-2);">
          {{ locale === 'zh' ? '暂无相关文章' : 'No related articles' }}
        </p>
      </template>
    </n-card>

    <n-result
      v-else
      status="404"
      :title="locale === 'zh' ? '文章未找到' : 'Article Not Found'"
      :description="locale === 'zh' ? '抱歉，找不到您要查找的文章。' : 'Sorry, the article you are looking for cannot be found.'"
    >
      <template #footer>
        <n-button @click="router.push(getRouterPathWithLang('/blog', locale))">
          {{ t('backToBlog') }}
        </n-button>
      </template>
    </n-result>
  </div>
</template>

<style scoped>
.blog-post-container {
  max-width: 900px;
  margin: 0 auto;
  padding: 24px;
}

.article-content {
  line-height: 1.8;
  font-size: 16px;
}

.article-content :deep(h1),
.article-content :deep(h2),
.article-content :deep(h3) {
  margin-top: 32px;
  margin-bottom: 16px;
}

.article-content :deep(p) {
  margin-bottom: 16px;
}

.article-content :deep(code) {
  background: var(--n-code-color);
  padding: 2px 6px;
  border-radius: 3px;
  font-family: 'Courier New', monospace;
}

.article-content :deep(pre) {
  background: var(--n-code-color);
  padding: 16px;
  border-radius: 6px;
  overflow-x: auto;
  margin: 16px 0;
}

.article-content :deep(ul),
.article-content :deep(ol) {
  margin-left: 24px;
  margin-bottom: 16px;
}

.article-content :deep(blockquote) {
  border-left: 4px solid var(--n-border-color);
  padding-left: 16px;
  margin: 16px 0;
  color: var(--n-text-color-2);
}
</style>
