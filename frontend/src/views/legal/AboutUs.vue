<template>
  <div class="about-page">
    <n-card>
      <template #header>
        <h1>{{ t('aboutUs') }}</h1>
      </template>

      <n-space vertical size="large">
        <section>
          <h2>{{ t('whoWeAre') }}</h2>
          <p>{{ t('whoWeAreDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('ourMission') }}</h2>
          <p>{{ t('missionDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('ourTechnology') }}</h2>
          <p>{{ t('techIntro') }}</p>
          
          <n-grid :cols="2" :x-gap="16" :y-gap="16" style="margin-top: 20px;">
            <n-gi>
              <n-card title="Cloudflare Workers" size="small">
                <p>{{ t('workersDesc') }}</p>
              </n-card>
            </n-gi>
            <n-gi>
              <n-card title="Rust WASM" size="small">
                <p>{{ t('wasmDesc') }}</p>
              </n-card>
            </n-gi>
            <n-gi>
              <n-card title="Cloudflare D1" size="small">
                <p>{{ t('d1Desc') }}</p>
              </n-card>
            </n-gi>
            <n-gi>
              <n-card title="Vue 3" size="small">
                <p>{{ t('vueDesc') }}</p>
              </n-card>
            </n-gi>
          </n-grid>
        </section>

        <section>
          <h2>{{ t('openSource') }}</h2>
          <p>{{ t('openSourceDesc') }}</p>
          <p>
            <n-button 
              tag="a" 
              href="https://github.com/dreamhunter2333/cloudflare_temp_email" 
              target="_blank"
              type="primary"
            >
              {{ t('viewOnGithub') }}
            </n-button>
          </p>
        </section>

        <section>
          <h2>{{ t('contactUs') }}</h2>
          <p>{{ t('contactDesc') }}</p>
          <p v-if="adminContact">
            <strong>{{ t('email') }}:</strong> 
            <a :href="`mailto:${adminContact}`">{{ adminContact }}</a>
          </p>
        </section>

        <section>
          <h2>{{ t('disclaimer') }}</h2>
          <n-alert type="warning" :show-icon="true">
            {{ t('disclaimerText') }}
          </n-alert>
        </section>
      </n-space>
    </n-card>
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'
import { useGlobalState } from '../../store'

const { t } = useI18n({
  messages: {
    en: {
      aboutUs: 'About Us',
      whoWeAre: 'Who We Are',
      whoWeAreDesc: 'We are a team of developers passionate about building privacy-focused tools and services. Our temporary email service is built on modern cloud infrastructure to provide fast, secure, and reliable email services.',
      
      ourMission: 'Our Mission',
      missionDesc: 'Our mission is to provide users with a secure, privacy-focused temporary email service while maintaining transparency and compliance with privacy regulations. We believe in open-source software and community-driven development.',
      
      ourTechnology: 'Our Technology',
      techIntro: 'We leverage cutting-edge technologies to deliver a high-performance email service:',
      workersDesc: 'Edge computing platform for global low-latency service delivery',
      wasmDesc: 'High-performance email parsing engine written in Rust',
      d1Desc: 'Lightweight SQLite database for reliable data storage',
      vueDesc: 'Modern frontend framework for responsive user interface',
      
      openSource: 'Open Source',
      openSourceDesc: 'This project is open source and available on GitHub under the MIT License. We welcome contributions from the community.',
      viewOnGithub: 'View on GitHub',
      
      contactUs: 'Contact Us',
      contactDesc: 'If you have any questions, suggestions, or feedback, please feel free to contact us:',
      email: 'Email',
      
      disclaimer: 'Disclaimer',
      disclaimerText: 'This service is provided as-is without any warranties. We are not affiliated with any educational institutions. Any .edu email addresses are temporary and for educational/testing purposes only.'
    },
    zh: {
      aboutUs: '关于我们',
      whoWeAre: '我们是谁',
      whoWeAreDesc: '我们是一群热衷于构建注重隐私的工具和服务的开发者。我们的临时邮箱服务建立在现代云基础设施之上，以提供快速、安全和可靠的邮件服务。',
      
      ourMission: '我们的使命',
      missionDesc: '我们的使命是在保持透明度和遵守隐私法规的同时，为用户提供安全、注重隐私的临时邮箱服务。我们相信开源软件和社区驱动的开发。',
      
      ourTechnology: '我们的技术',
      techIntro: '我们利用尖端技术提供高性能的邮件服务：',
      workersDesc: '边缘计算平台，提供全球低延迟服务',
      wasmDesc: '用 Rust 编写的高性能邮件解析引擎',
      d1Desc: '轻量级 SQLite 数据库，用于可靠的数据存储',
      vueDesc: '现代前端框架，提供响应式用户界面',
      
      openSource: '开源',
      openSourceDesc: '本项目是开源的，在 GitHub 上以 MIT 许可证提供。我们欢迎社区的贡献。',
      viewOnGithub: '在 GitHub 上查看',
      
      contactUs: '联系我们',
      contactDesc: '如果您有任何问题、建议或反馈，请随时联系我们：',
      email: '邮箱',
      
      disclaimer: '免责声明',
      disclaimerText: '本服务按现状提供，不提供任何保证。我们不隶属于任何教育机构。任何 .edu 邮箱地址都是临时的，仅用于教育/测试目的。'
    }
  }
})

const { openSettings } = useGlobalState()
const adminContact = computed(() => openSettings.value?.adminContact)
</script>

<style scoped>
.about-page {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}

.about-page h1 {
  margin: 0 0 10px 0;
  font-size: 28px;
}

.about-page h2 {
  margin-top: 30px;
  margin-bottom: 15px;
  font-size: 22px;
  color: var(--n-text-color);
}

.about-page p {
  line-height: 1.8;
  margin-bottom: 15px;
}

.about-page a {
  color: var(--n-primary-color);
  text-decoration: none;
}

.about-page a:hover {
  text-decoration: underline;
}

section {
  margin-bottom: 30px;
}
</style>
