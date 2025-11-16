<template>
  <div class="legal-page">
    <n-card>
      <template #header>
        <h1>{{ t('privacyPolicy') }}</h1>
        <n-text depth="3">{{ t('lastUpdated') }}: {{ lastUpdated }}</n-text>
      </template>

      <n-space vertical size="large">
        <section>
          <h2>{{ t('introduction') }}</h2>
          <p>{{ t('privacyIntro') }}</p>
        </section>

        <section>
          <h2>{{ t('informationWeCollect') }}</h2>
          <h3>{{ t('emailData') }}</h3>
          <p>{{ t('emailDataDesc') }}</p>
          
          <h3>{{ t('usageData') }}</h3>
          <p>{{ t('usageDataDesc') }}</p>
          
          <h3>{{ t('cookiesAndTracking') }}</h3>
          <p>{{ t('cookiesDesc') }}</p>
          <p>{{ t('googleAdsDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('howWeUseInformation') }}</h2>
          <ul>
            <li>{{ t('usePurpose1') }}</li>
            <li>{{ t('usePurpose2') }}</li>
            <li>{{ t('usePurpose3') }}</li>
            <li>{{ t('usePurpose4') }}</li>
          </ul>
        </section>

        <section>
          <h2>{{ t('dataStorage') }}</h2>
          <p>{{ t('dataStorageDesc') }}</p>
          <p>{{ t('dataRetention') }}</p>
        </section>

        <section>
          <h2>{{ t('dataSecurity') }}</h2>
          <p>{{ t('securityMeasures') }}</p>
        </section>

        <section>
          <h2>{{ t('thirdPartyServices') }}</h2>
          <h3>{{ t('googleAdsense') }}</h3>
          <p>{{ t('googleAdsenseDesc') }}</p>
          <p>
            <a href="https://policies.google.com/privacy" target="_blank" rel="noopener noreferrer">
              {{ t('googlePrivacyPolicy') }}
            </a>
          </p>
          
          <h3>{{ t('cloudflare') }}</h3>
          <p>{{ t('cloudflareDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('yourRights') }}</h2>
          <p>{{ t('rightsDesc') }}</p>
          <ul>
            <li>{{ t('right1') }}</li>
            <li>{{ t('right2') }}</li>
            <li>{{ t('right3') }}</li>
            <li>{{ t('right4') }}</li>
          </ul>
        </section>

        <section>
          <h2>{{ t('childrenPrivacy') }}</h2>
          <p>{{ t('childrenPrivacyDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('changesToPolicy') }}</h2>
          <p>{{ t('policyChangesDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('contactUs') }}</h2>
          <p>{{ t('contactDesc') }}</p>
          <p v-if="adminContact">
            <strong>{{ t('email') }}:</strong> 
            <a :href="`mailto:${adminContact}`">{{ adminContact }}</a>
          </p>
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
      privacyPolicy: 'Privacy Policy',
      lastUpdated: 'Last Updated',
      introduction: '1. Introduction',
      privacyIntro: 'We are committed to protecting your privacy. This Privacy Policy explains how we collect, use, disclose, and safeguard your information when you use our temporary email service.',
      
      informationWeCollect: '2. Information We Collect',
      emailData: 'Email Data',
      emailDataDesc: 'Our service temporarily stores emails sent to temporary email addresses you create. These emails are stored securely and automatically deleted according to our retention policies.',
      usageData: 'Usage Data',
      usageDataDesc: 'We collect information about how you interact with our service, including IP addresses, browser type, access times, and pages viewed.',
      cookiesAndTracking: 'Cookies and Tracking Technologies',
      cookiesDesc: 'We use cookies and similar tracking technologies to maintain your session, remember your preferences, and improve our service.',
      googleAdsDesc: 'We use Google AdSense to display advertisements. Google may use cookies and other tracking technologies to personalize ads and measure ad performance. For more information, please review Google\'s Privacy Policy.',
      
      howWeUseInformation: '3. How We Use Your Information',
      usePurpose1: 'To provide and maintain our temporary email service',
      usePurpose2: 'To improve and optimize our service',
      usePurpose3: 'To analyze usage patterns and trends',
      usePurpose4: 'To comply with legal obligations',
      
      dataStorage: '4. Data Storage',
      dataStorageDesc: 'Your data is stored on Cloudflare\'s infrastructure, including D1 databases, KV storage, and R2 object storage.',
      dataRetention: 'Temporary emails are automatically deleted after a specified retention period. You can manually delete emails at any time.',
      
      dataSecurity: '5. Data Security',
      securityMeasures: 'We implement industry-standard security measures to protect your data, including encryption, secure access controls, and regular security audits.',
      
      thirdPartyServices: '6. Third-Party Services',
      googleAdsense: 'Google AdSense',
      googleAdsenseDesc: 'We use Google AdSense to display advertisements on our website. Google may collect and use data according to their privacy policy.',
      googlePrivacyPolicy: 'Google Privacy Policy',
      cloudflare: 'Cloudflare',
      cloudflareDesc: 'Our service is hosted on Cloudflare\'s infrastructure. Please refer to Cloudflare\'s Privacy Policy for information about their data practices.',
      
      yourRights: '7. Your Rights',
      rightsDesc: 'You have the right to:',
      right1: 'Access your personal data',
      right2: 'Request deletion of your data',
      right3: 'Opt-out of certain data collection',
      right4: 'File a complaint with relevant authorities',
      
      childrenPrivacy: '8. Children\'s Privacy',
      childrenPrivacyDesc: 'Our service is not intended for children under 13 years of age. We do not knowingly collect personal information from children.',
      
      changesToPolicy: '9. Changes to This Privacy Policy',
      policyChangesDesc: 'We may update this Privacy Policy from time to time. We will notify you of any changes by posting the new Privacy Policy on this page.',
      
      contactUs: '10. Contact Us',
      contactDesc: 'If you have any questions about this Privacy Policy, please contact us:',
      email: 'Email'
    },
    zh: {
      privacyPolicy: '隐私政策',
      lastUpdated: '最后更新',
      introduction: '1. 介绍',
      privacyIntro: '我们致力于保护您的隐私。本隐私政策说明了当您使用我们的临时邮箱服务时，我们如何收集、使用、披露和保护您的信息。',
      
      informationWeCollect: '2. 我们收集的信息',
      emailData: '邮件数据',
      emailDataDesc: '我们的服务会临时存储发送到您创建的临时邮箱地址的邮件。这些邮件会被安全存储，并根据我们的保留政策自动删除。',
      usageData: '使用数据',
      usageDataDesc: '我们收集有关您如何使用我们服务的信息，包括 IP 地址、浏览器类型、访问时间和查看的页面。',
      cookiesAndTracking: 'Cookie 和跟踪技术',
      cookiesDesc: '我们使用 Cookie 和类似的跟踪技术来维护您的会话、记住您的偏好并改进我们的服务。',
      googleAdsDesc: '我们使用 Google AdSense 来显示广告。Google 可能使用 Cookie 和其他跟踪技术来个性化广告并衡量广告效果。更多信息，请查看 Google 的隐私政策。',
      
      howWeUseInformation: '3. 我们如何使用您的信息',
      usePurpose1: '提供和维护我们的临时邮箱服务',
      usePurpose2: '改进和优化我们的服务',
      usePurpose3: '分析使用模式和趋势',
      usePurpose4: '遵守法律义务',
      
      dataStorage: '4. 数据存储',
      dataStorageDesc: '您的数据存储在 Cloudflare 的基础设施上，包括 D1 数据库、KV 存储和 R2 对象存储。',
      dataRetention: '临时邮件会在指定的保留期后自动删除。您可以随时手动删除邮件。',
      
      dataSecurity: '5. 数据安全',
      securityMeasures: '我们实施行业标准的安全措施来保护您的数据，包括加密、安全访问控制和定期安全审计。',
      
      thirdPartyServices: '6. 第三方服务',
      googleAdsense: 'Google AdSense',
      googleAdsenseDesc: '我们使用 Google AdSense 在我们的网站上显示广告。Google 可能会根据其隐私政策收集和使用数据。',
      googlePrivacyPolicy: 'Google 隐私政策',
      cloudflare: 'Cloudflare',
      cloudflareDesc: '我们的服务托管在 Cloudflare 的基础设施上。有关其数据实践的信息，请参阅 Cloudflare 的隐私政策。',
      
      yourRights: '7. 您的权利',
      rightsDesc: '您有权：',
      right1: '访问您的个人数据',
      right2: '请求删除您的数据',
      right3: '选择退出某些数据收集',
      right4: '向相关当局投诉',
      
      childrenPrivacy: '8. 儿童隐私',
      childrenPrivacyDesc: '我们的服务不适用于 13 岁以下的儿童。我们不会故意收集儿童的个人信息。',
      
      changesToPolicy: '9. 隐私政策的变更',
      policyChangesDesc: '我们可能会不时更新本隐私政策。我们会在本页面上发布新的隐私政策来通知您任何变更。',
      
      contactUs: '10. 联系我们',
      contactDesc: '如果您对本隐私政策有任何疑问，请联系我们：',
      email: '邮箱'
    }
  }
})

const { openSettings } = useGlobalState()
const adminContact = computed(() => openSettings.value?.adminContact)

const lastUpdated = '2025-01-27'
</script>

<style scoped>
.legal-page {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}

.legal-page h1 {
  margin: 0 0 10px 0;
  font-size: 28px;
}

.legal-page h2 {
  margin-top: 30px;
  margin-bottom: 15px;
  font-size: 22px;
  color: var(--n-text-color);
}

.legal-page h3 {
  margin-top: 20px;
  margin-bottom: 10px;
  font-size: 18px;
  color: var(--n-text-color);
}

.legal-page p {
  line-height: 1.8;
  margin-bottom: 15px;
}

.legal-page ul {
  line-height: 1.8;
  padding-left: 20px;
}

.legal-page li {
  margin-bottom: 8px;
}

.legal-page a {
  color: var(--n-primary-color);
  text-decoration: none;
}

.legal-page a:hover {
  text-decoration: underline;
}

section {
  margin-bottom: 30px;
}
</style>
