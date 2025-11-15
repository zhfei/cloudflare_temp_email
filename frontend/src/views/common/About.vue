<script setup>
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
import { useRouter } from 'vue-router'
import { useHead } from '@unhead/vue'
import { GithubAlt, Discord, Telegram } from '@vicons/fa'
import { useGlobalState } from '../../store'
import { getRouterPathWithLang } from '../../utils'
import { useIsMobile } from '../../utils/composables'

const isMobile = useIsMobile()

const { announcement, openSettings } = useGlobalState()
const router = useRouter()

const { locale, t } = useI18n({
  messages: {
    en: {
      title: 'About',
      subtitle: 'A high-performance temporary email service built on Cloudflare',
      mission: 'Our Mission',
      missionText: 'To provide a secure, privacy-focused temporary email service while educating users about email security, privacy protection, and modern web technologies.',
      technology: 'Technology',
      technologyText: 'Built with cutting-edge serverless technologies including Cloudflare Workers, D1 database, Rust WebAssembly, and modern web frameworks.',
      features: 'Key Features',
      learnMore: 'Learn More',
      viewBlog: 'View Blog',
      viewResources: 'View Resources',
      disclaimer: 'Important Disclaimer',
      disclaimerText: 'This service provides temporary email addresses for technical demonstration and educational purposes only. We are not affiliated with any educational institutions, organizations, or domain registrars. Please use this service responsibly and in compliance with all applicable laws and regulations.',
      community: 'Community'
    },
    zh: {
      title: '关于我们',
      subtitle: '基于 Cloudflare 构建的高性能临时邮件服务',
      mission: '我们的使命',
      missionText: '提供安全、注重隐私的临时邮件服务，同时教育用户了解邮件安全、隐私保护和现代 Web 技术。',
      technology: '技术',
      technologyText: '使用前沿的无服务器技术构建，包括 Cloudflare Workers、D1 数据库、Rust WebAssembly 和现代 Web 框架。',
      features: '核心功能',
      learnMore: '了解更多',
      viewBlog: '查看博客',
      viewResources: '查看资源',
      disclaimer: '重要免责声明',
      disclaimerText: '本服务提供的临时邮箱地址仅用于技术演示和教育目的。我们与任何教育机构、组织或域名注册机构没有关联。请负责任地使用本服务，并遵守所有适用的法律法规。',
      community: '社区'
    }
  }
})

useHead({
  title: t('title'),
  meta: [
    { name: 'description', content: t('subtitle') }
  ]
})

const features = ref([
  {
    title: { en: 'Serverless Architecture', zh: '无服务器架构' },
    desc: { en: 'Built on Cloudflare Workers for zero infrastructure costs', zh: '基于 Cloudflare Workers 构建，零基础设施成本' }
  },
  {
    title: { en: 'High Performance', zh: '高性能' },
    desc: { en: 'Rust WASM email parsing for fast and reliable processing', zh: 'Rust WASM 邮件解析，快速可靠的处理' }
  },
  {
    title: { en: 'Privacy Focused', zh: '注重隐私' },
    desc: { en: 'Automatic email cleanup and privacy protection features', zh: '自动邮件清理和隐私保护功能' }
  },
  {
    title: { en: 'Open Source', zh: '开源' },
    desc: { en: 'Fully open source and community-driven development', zh: '完全开源，社区驱动开发' }
  }
])

const goToPage = (path) => {
  router.push(getRouterPathWithLang(path, locale.value))
}
</script>

<template>
    <div class="about-container">
        <n-card :bordered="false">
            <div class="about-header">
                <h1>{{ t('title') }}</h1>
                <p class="subtitle">{{ t('subtitle') }}</p>
            </div>

            <n-divider />

            <!-- 使命 -->
            <n-space vertical size="large">
                <div>
                    <h2>{{ t('mission') }}</h2>
                    <p>{{ t('missionText') }}</p>
                </div>

                <!-- 技术 -->
                <div>
                    <h2>{{ t('technology') }}</h2>
                    <p>{{ t('technologyText') }}</p>
                    <n-space style="margin-top: 16px;">
                        <n-button type="primary" @click="goToPage('/blog')">
                            {{ t('viewBlog') }}
                        </n-button>
                        <n-button @click="goToPage('/resources')">
                            {{ t('viewResources') }}
                        </n-button>
                    </n-space>
                </div>

                <!-- 核心功能 -->
                <div>
                    <h2>{{ t('features') }}</h2>
                    <n-grid :cols="isMobile ? 1 : 2" :x-gap="16" :y-gap="16" style="margin-top: 16px;">
                        <n-gi v-for="feature in features" :key="feature.title.en">
                            <n-card>
                                <h3 style="margin-top: 0;">{{ feature.title[locale] }}</h3>
                                <p style="color: var(--n-text-color-2);">{{ feature.desc[locale] }}</p>
                            </n-card>
                        </n-gi>
                    </n-grid>
                </div>

                <!-- 免责声明 -->
                <n-alert type="warning" :title="t('disclaimer')">
                    {{ t('disclaimerText') }}
                </n-alert>

                <!-- 公告 -->
                <div v-if="announcement">
                    <div v-html="announcement"></div>
                </div>

                <!-- 社区链接 -->
                <div>
                    <h2>{{ t('community') }}</h2>
                    <n-space>
                        <n-button tag="a" target="_blank" href="https://github.com/dreamhunter2333/cloudflare_temp_email">
                            <template #icon>
                                <n-icon :component="GithubAlt" />
                            </template>
                            Github
                        </n-button>
                        <n-button tag="a" target="_blank" href="https://discord.gg/dQEwTWhA6Q">
                            <template #icon>
                                <n-icon :component="Discord" />
                            </template>
                            Discord
                        </n-button>
                        <n-button tag="a" target="_blank" href="https://t.me/cloudflare_temp_email">
                            <template #icon>
                                <n-icon :component="Telegram" />
                            </template>
                            Telegram
                        </n-button>
                    </n-space>
                </div>

                <!-- 联系方式 -->
                <div v-if="openSettings?.adminContact">
                    <h2>{{ locale === 'zh' ? '联系我们' : 'Contact Us' }}</h2>
                    <n-text>{{ openSettings.adminContact }}</n-text>
                </div>
            </n-space>
        </n-card>
    </div>
</template>

<style scoped>
.about-container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 24px;
}

.about-header {
    text-align: center;
    margin-bottom: 24px;
}

.about-header h1 {
    font-size: 2.5em;
    margin-bottom: 12px;
}

.subtitle {
    font-size: 1.2em;
    color: var(--n-text-color-2);
}

.about-container h2 {
    margin-top: 32px;
    margin-bottom: 16px;
    font-size: 1.5em;
}

.about-container h3 {
    margin-top: 16px;
    margin-bottom: 8px;
    font-size: 1.2em;
}

.about-container p {
    line-height: 1.8;
    margin-bottom: 16px;
}
</style>
