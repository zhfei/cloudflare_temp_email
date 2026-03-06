<template>
  <div class="security-page">
    <n-card>
      <template #header>
        <h1>{{ t('privacyAndSecurity') }}</h1>
        <n-text depth="3">{{ t('securitySubtitle') }}</n-text>
      </template>
      <AdsterraNativeBanner />
      <n-space vertical size="large">
        <section>
          <h2>{{ t('emailSecurity') }}</h2>
          <p>{{ t('emailSecurityDesc') }}</p>
          
          <n-grid :cols="2" :x-gap="16" :y-gap="16" style="margin-top: 20px;">
            <n-gi>
              <n-card title="SPF Verification" size="small">
                <p>{{ t('spfDesc') }}</p>
              </n-card>
            </n-gi>
            <n-gi>
              <n-card title="DKIM Verification" size="small">
                <p>{{ t('dkimDesc') }}</p>
              </n-card>
            </n-gi>
            <n-gi>
              <n-card title="DMARC Verification" size="small">
                <p>{{ t('dmarcDesc') }}</p>
              </n-card>
            </n-gi>
            <n-gi>
              <n-card title="Spam Detection" size="small">
                <p>{{ t('spamDesc') }}</p>
              </n-card>
            </n-gi>
          </n-grid>
        </section>

        <section>
          <h2>{{ t('dataProtection') }}</h2>
          <p>{{ t('dataProtectionDesc') }}</p>
          
          <h3>{{ t('encryption') }}</h3>
          <ul>
            <li>{{ t('encryption1') }}</li>
            <li>{{ t('encryption2') }}</li>
            <li>{{ t('encryption3') }}</li>
          </ul>
          
          <h3>{{ t('accessControl') }}</h3>
          <ul>
            <li>{{ t('accessControl1') }}</li>
            <li>{{ t('accessControl2') }}</li>
            <li>{{ t('accessControl3') }}</li>
          </ul>
        </section>

        <section>
          <h2>{{ t('emailTracking') }}</h2>
          <p>{{ t('trackingDesc') }}</p>
          
          <h3>{{ t('trackingMethods') }}</h3>
          <ul>
            <li><strong>{{ t('pixelTracking') }}:</strong> {{ t('pixelTrackingDesc') }}</li>
            <li><strong>{{ t('linkTracking') }}:</strong> {{ t('linkTrackingDesc') }}</li>
            <li><strong>{{ t('readReceipts') }}:</strong> {{ t('readReceiptsDesc') }}</li>
          </ul>
          
          <h3>{{ t('ourProtection') }}</h3>
          <ul>
            <li>{{ t('protection1') }}</li>
            <li>{{ t('protection2') }}</li>
            <li>{{ t('protection3') }}</li>
            <li>{{ t('protection4') }}</li>
          </ul>
        </section>

        <section>
          <h2>{{ t('privacyRights') }}</h2>
          <p>{{ t('privacyRightsDesc') }}</p>
          
          <n-list>
            <n-list-item>
              <template #prefix>
                <n-icon :component="CheckmarkCircle" />
              </template>
              <n-text strong>{{ t('right1') }}</n-text>
              <template #suffix>
                <n-text depth="3">{{ t('right1Desc') }}</n-text>
              </template>
            </n-list-item>
            <n-list-item>
              <template #prefix>
                <n-icon :component="CheckmarkCircle" />
              </template>
              <n-text strong>{{ t('right2') }}</n-text>
              <template #suffix>
                <n-text depth="3">{{ t('right2Desc') }}</n-text>
              </template>
            </n-list-item>
            <n-list-item>
              <template #prefix>
                <n-icon :component="CheckmarkCircle" />
              </template>
              <n-text strong>{{ t('right3') }}</n-text>
              <template #suffix>
                <n-text depth="3">{{ t('right3Desc') }}</n-text>
              </template>
            </n-list-item>
            <n-list-item>
              <template #prefix>
                <n-icon :component="CheckmarkCircle" />
              </template>
              <n-text strong>{{ t('right4') }}</n-text>
              <template #suffix>
                <n-text depth="3">{{ t('right4Desc') }}</n-text>
              </template>
            </n-list-item>
          </n-list>
        </section>

        <section>
          <h2>{{ t('compliance') }}</h2>
          <p>{{ t('complianceDesc') }}</p>
          
          <n-alert type="info" :show-icon="true">
            {{ t('complianceNotice') }}
          </n-alert>
        </section>

        <section>
          <h2>{{ t('reportingIssues') }}</h2>
          <p>{{ t('reportingDesc') }}</p>
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
import { CheckmarkCircle } from '@vicons/ionicons5'
import { useGlobalState } from '../../store'
import AdsterraNativeBanner from '../../components/AdsterraNativeBanner.vue';

const { t } = useI18n({
  messages: {
    en: {
      privacyAndSecurity: 'Privacy & Security',
      securitySubtitle: 'Learn about our security measures and privacy protections',
      
      emailSecurity: 'Email Security',
      emailSecurityDesc: 'We implement multiple layers of email security to protect against spam, phishing, and malicious content.',
      spfDesc: 'Sender Policy Framework verification ensures emails come from authorized servers',
      dkimDesc: 'DomainKeys Identified Mail verification confirms email authenticity',
      dmarcDesc: 'Domain-based Message Authentication prevents email spoofing',
      spamDesc: 'Advanced spam detection using multiple heuristics and blacklists',
      
      dataProtection: 'Data Protection',
      dataProtectionDesc: 'Your data is protected through multiple security measures:',
      encryption: 'Encryption',
      encryption1: 'TLS/SSL encryption for data in transit',
      encryption2: 'Encrypted storage for sensitive data',
      encryption3: 'Secure key management and rotation',
      accessControl: 'Access Control',
      accessControl1: 'JWT-based authentication',
      accessControl2: 'Role-based access control',
      accessControl3: 'IP-based rate limiting',
      
      emailTracking: 'Email Tracking Protection',
      trackingDesc: 'Email tracking is a common practice used by marketers and spammers to monitor when and where emails are opened.',
      trackingMethods: 'Common Tracking Methods',
      pixelTracking: 'Pixel Tracking',
      pixelTrackingDesc: 'Invisible 1x1 images that report back when opened',
      linkTracking: 'Link Tracking',
      linkTrackingDesc: 'Redirect URLs that track click-through rates',
      readReceipts: 'Read Receipts',
      readReceiptsDesc: 'Requests for delivery and read confirmations',
      ourProtection: 'Our Protection Measures',
      protection1: 'Automatic image proxying to prevent pixel tracking',
      protection2: 'Link sanitization and warning system',
      protection3: 'Email content analysis for tracking indicators',
      protection4: 'User education and awareness',
      
      privacyRights: 'Your Privacy Rights',
      privacyRightsDesc: 'You have the following rights regarding your personal data:',
      right1: 'Right to Access',
      right1Desc: 'View all data we have about you',
      right2: 'Right to Deletion',
      right2Desc: 'Request deletion of your data',
      right3: 'Right to Portability',
      right3Desc: 'Export your data in a portable format',
      right4: 'Right to Object',
      right4Desc: 'Opt-out of certain data processing',
      
      compliance: 'Compliance',
      complianceDesc: 'We are committed to complying with privacy regulations and industry standards.',
      complianceNotice: 'We follow GDPR, CCPA, and other applicable privacy regulations. Our data handling practices are transparent and user-focused.',
      
      reportingIssues: 'Reporting Security Issues',
      reportingDesc: 'If you discover a security vulnerability, please report it responsibly:',
      email: 'Email'
    },
    zh: {
      privacyAndSecurity: '隐私与安全',
      securitySubtitle: '了解我们的安全措施和隐私保护',
      
      emailSecurity: '邮件安全',
      emailSecurityDesc: '我们实施多层邮件安全措施，以防范垃圾邮件、钓鱼和恶意内容。',
      spfDesc: 'SPF 验证确保邮件来自授权服务器',
      dkimDesc: 'DKIM 验证确认邮件真实性',
      dmarcDesc: 'DMARC 防止邮件伪造',
      spamDesc: '使用多种启发式方法和黑名单的高级垃圾邮件检测',
      
      dataProtection: '数据保护',
      dataProtectionDesc: '您的数据通过多种安全措施得到保护：',
      encryption: '加密',
      encryption1: '传输数据的 TLS/SSL 加密',
      encryption2: '敏感数据的加密存储',
      encryption3: '安全的密钥管理和轮换',
      accessControl: '访问控制',
      accessControl1: '基于 JWT 的身份验证',
      accessControl2: '基于角色的访问控制',
      accessControl3: '基于 IP 的速率限制',
      
      emailTracking: '邮件跟踪保护',
      trackingDesc: '邮件跟踪是营销人员和垃圾邮件发送者用来监控邮件何时何地被打开的常见做法。',
      trackingMethods: '常见的跟踪方法',
      pixelTracking: '像素跟踪',
      pixelTrackingDesc: '打开时报告回传的不可见 1x1 图像',
      linkTracking: '链接跟踪',
      linkTrackingDesc: '跟踪点击率的重定向 URL',
      readReceipts: '已读回执',
      readReceiptsDesc: '请求传递和已读确认',
      ourProtection: '我们的保护措施',
      protection1: '自动图像代理以防止像素跟踪',
      protection2: '链接清理和警告系统',
      protection3: '邮件内容分析以检测跟踪指标',
      protection4: '用户教育和意识',
      
      privacyRights: '您的隐私权',
      privacyRightsDesc: '您对个人数据拥有以下权利：',
      right1: '访问权',
      right1Desc: '查看我们拥有的所有关于您的数据',
      right2: '删除权',
      right2Desc: '请求删除您的数据',
      right3: '可移植权',
      right3Desc: '以可移植格式导出您的数据',
      right4: '反对权',
      right4Desc: '选择退出某些数据处理',
      
      compliance: '合规性',
      complianceDesc: '我们致力于遵守隐私法规和行业标准。',
      complianceNotice: '我们遵循 GDPR、CCPA 和其他适用的隐私法规。我们的数据处理实践是透明且以用户为中心的。',
      
      reportingIssues: '报告安全问题',
      reportingDesc: '如果您发现安全漏洞，请负责任地报告：',
      email: '邮箱'
    }
  }
})

const { openSettings } = useGlobalState()
const adminContact = computed(() => openSettings.value?.adminContact)
</script>

<style scoped>
.security-page {
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
}

.security-page h1 {
  margin: 0 0 10px 0;
  font-size: 28px;
}

.security-page h2 {
  margin-top: 30px;
  margin-bottom: 15px;
  font-size: 22px;
  color: var(--n-text-color);
}

.security-page h3 {
  margin-top: 20px;
  margin-bottom: 10px;
  font-size: 18px;
  color: var(--n-text-color);
}

.security-page p {
  line-height: 1.8;
  margin-bottom: 15px;
}

.security-page ul {
  line-height: 1.8;
  padding-left: 20px;
}

.security-page li {
  margin-bottom: 8px;
}

.security-page a {
  color: var(--n-primary-color);
  text-decoration: none;
}

.security-page a:hover {
  text-decoration: underline;
}

section {
  margin-bottom: 30px;
}
</style>
