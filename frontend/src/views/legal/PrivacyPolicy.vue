<script setup>
import { useI18n } from 'vue-i18n'
import { useHead } from '@unhead/vue'

const { locale, t } = useI18n({
  messages: {
    en: {
      title: 'Privacy Policy',
      lastUpdated: 'Last Updated',
      effectiveDate: 'Effective Date'
    },
    zh: {
      title: '隐私政策',
      lastUpdated: '最后更新',
      effectiveDate: '生效日期'
    }
  }
})

useHead({
  title: t('title')
})

const lastUpdated = '2024-02-15'
const effectiveDate = '2024-01-01'
</script>

<template>
  <div class="legal-container">
    <n-card :bordered="false">
      <h1>{{ t('title') }}</h1>
      
      <n-space style="margin: 16px 0;" vertical>
        <n-text depth="3">
          {{ t('lastUpdated') }}: {{ lastUpdated }}
        </n-text>
        <n-text depth="3">
          {{ t('effectiveDate') }}: {{ effectiveDate }}
        </n-text>
      </n-space>

      <n-divider />

      <div class="legal-content">
        <template v-if="locale === 'zh'">
          <h2>1. 信息收集</h2>
          <p>我们收集以下类型的信息：</p>
          <ul>
            <li><strong>邮件内容</strong>：当您使用我们的临时邮箱服务时，我们会临时存储发送到您邮箱地址的邮件内容。这些邮件仅用于显示给您，我们不会读取或分析邮件内容。</li>
            <li><strong>技术信息</strong>：我们收集访问日志、IP地址、浏览器类型等匿名技术信息，用于改善服务质量和防止滥用。</li>
            <li><strong>Cookie和本地存储</strong>：我们使用Cookie和本地存储来保存您的偏好设置和登录状态。</li>
          </ul>

          <h2>2. 信息使用</h2>
          <p>我们使用收集的信息用于：</p>
          <ul>
            <li>提供和维护临时邮箱服务</li>
            <li>改善用户体验和服务质量</li>
            <li>防止服务滥用和确保安全性</li>
            <li>遵守法律法规要求</li>
          </ul>

          <h2>3. Google广告服务</h2>
          <p>本网站使用Google AdSense广告服务。Google及其合作伙伴使用Cookie来根据您访问本网站和其他网站的情况投放广告。您可以通过访问<a href="https://www.google.com/settings/ads" target="_blank">Google广告设置</a>来选择退出个性化广告。</p>
          <p>我们使用Google Analytics来了解网站使用情况。Google Analytics使用Cookie来收集匿名使用数据。您可以安装<a href="https://tools.google.com/dlpage/gaoptout" target="_blank">Google Analytics退出插件</a>来阻止Google Analytics收集您的数据。</p>

          <h2>4. 信息共享</h2>
          <p>我们不会出售、交易或转让您的个人信息给第三方，除非：</p>
          <ul>
            <li>您明确同意</li>
            <li>法律要求或法院命令</li>
            <li>保护我们的权利、财产或安全</li>
            <li>与服务提供商共享（如云存储服务），这些服务提供商有义务保护您的信息</li>
          </ul>

          <h2>5. 数据安全</h2>
          <p>我们采用行业标准的安全措施来保护您的信息，包括：</p>
          <ul>
            <li>SSL/TLS加密传输</li>
            <li>定期安全审计</li>
            <li>访问控制和身份验证</li>
            <li>自动数据清理机制</li>
          </ul>

          <h2>6. 数据保留</h2>
          <p>临时邮箱中的邮件会根据我们的数据保留政策自动删除。默认情况下，邮件会在一定时间后自动清理。您可以随时删除您的邮箱地址和相关邮件。</p>

          <h2>7. 您的权利</h2>
          <p>您有权：</p>
          <ul>
            <li>访问和查看我们存储的您的信息</li>
            <li>要求删除您的个人信息</li>
            <li>选择退出某些数据收集</li>
            <li>提出投诉或询问</li>
          </ul>

          <h2>8. 第三方服务</h2>
          <p>我们的服务可能包含指向第三方网站的链接。我们不对这些网站的隐私做法负责。我们建议您阅读这些网站的隐私政策。</p>

          <h2>9. 儿童隐私</h2>
          <p>我们的服务不面向13岁以下的儿童。我们不会故意收集13岁以下儿童的个人信息。如果发现我们收集了此类信息，我们将立即删除。</p>

          <h2>10. 政策变更</h2>
          <p>我们可能会不时更新本隐私政策。重大变更将在网站上发布通知。继续使用我们的服务即表示您接受更新后的政策。</p>

          <h2>11. 联系我们</h2>
          <p>如果您对本隐私政策有任何问题或疑虑，请通过以下方式联系我们：</p>
          <ul>
            <li>通过网站上的"联系我们"页面</li>
            <li>发送邮件至管理员邮箱（如已配置）</li>
          </ul>

          <h2>12. 免责声明</h2>
          <p><strong>重要提示</strong>：本服务提供的临时邮箱地址（包括但不限于.edu域名邮箱）仅用于技术演示和教育目的。我们与任何教育机构、组织或域名注册机构没有关联。使用本服务时，请遵守所有适用的法律法规和网站服务条款。</p>
        </template>

        <template v-else>
          <h2>1. Information We Collect</h2>
          <p>We collect the following types of information:</p>
          <ul>
            <li><strong>Email Content</strong>: When you use our temporary email service, we temporarily store email content sent to your email address. These emails are only displayed to you, and we do not read or analyze email content.</li>
            <li><strong>Technical Information</strong>: We collect anonymous technical information such as access logs, IP addresses, browser types, etc., to improve service quality and prevent abuse.</li>
            <li><strong>Cookies and Local Storage</strong>: We use cookies and local storage to save your preferences and login status.</li>
          </ul>

          <h2>2. How We Use Information</h2>
          <p>We use the collected information to:</p>
          <ul>
            <li>Provide and maintain temporary email services</li>
            <li>Improve user experience and service quality</li>
            <li>Prevent service abuse and ensure security</li>
            <li>Comply with legal requirements</li>
          </ul>

          <h2>3. Google Advertising Services</h2>
          <p>This website uses Google AdSense advertising service. Google and its partners use cookies to serve ads based on your visits to this site and other sites. You can opt out of personalized advertising by visiting <a href="https://www.google.com/settings/ads" target="_blank">Google's Ad Settings</a>.</p>
          <p>We use Google Analytics to understand website usage. Google Analytics uses cookies to collect anonymous usage data. You can install the <a href="https://tools.google.com/dlpage/gaoptout" target="_blank">Google Analytics Opt-out Browser Add-on</a> to prevent Google Analytics from collecting your data.</p>

          <h2>4. Information Sharing</h2>
          <p>We do not sell, trade, or transfer your personal information to third parties, except:</p>
          <ul>
            <li>With your explicit consent</li>
            <li>As required by law or court order</li>
            <li>To protect our rights, property, or safety</li>
            <li>With service providers (such as cloud storage services) who are obligated to protect your information</li>
          </ul>

          <h2>5. Data Security</h2>
          <p>We employ industry-standard security measures to protect your information, including:</p>
          <ul>
            <li>SSL/TLS encrypted transmission</li>
            <li>Regular security audits</li>
            <li>Access controls and authentication</li>
            <li>Automatic data cleanup mechanisms</li>
          </ul>

          <h2>6. Data Retention</h2>
          <p>Emails in temporary mailboxes are automatically deleted according to our data retention policy. By default, emails are automatically cleaned up after a certain period. You can delete your email address and related emails at any time.</p>

          <h2>7. Your Rights</h2>
          <p>You have the right to:</p>
          <ul>
            <li>Access and view your information stored by us</li>
            <li>Request deletion of your personal information</li>
            <li>Opt out of certain data collection</li>
            <li>File complaints or inquiries</li>
          </ul>

          <h2>8. Third-Party Services</h2>
          <p>Our service may contain links to third-party websites. We are not responsible for the privacy practices of these websites. We recommend reading the privacy policies of these websites.</p>

          <h2>9. Children's Privacy</h2>
          <p>Our service is not directed to children under 13. We do not knowingly collect personal information from children under 13. If we discover that we have collected such information, we will delete it immediately.</p>

          <h2>10. Policy Changes</h2>
          <p>We may update this privacy policy from time to time. Significant changes will be notified on the website. Continued use of our service indicates acceptance of the updated policy.</p>

          <h2>11. Contact Us</h2>
          <p>If you have any questions or concerns about this privacy policy, please contact us through:</p>
          <ul>
            <li>The "Contact Us" page on the website</li>
            <li>Email to the administrator (if configured)</li>
          </ul>

          <h2>12. Disclaimer</h2>
          <p><strong>Important Notice</strong>: The temporary email addresses provided by this service (including but not limited to .edu domain emails) are for technical demonstration and educational purposes only. We are not affiliated with any educational institutions, organizations, or domain registrars. When using this service, please comply with all applicable laws, regulations, and website terms of service.</p>
        </template>
      </div>
    </n-card>
  </div>
</template>

<style scoped>
.legal-container {
  max-width: 900px;
  margin: 0 auto;
  padding: 24px;
}

.legal-content {
  line-height: 1.8;
}

.legal-content h2 {
  margin-top: 32px;
  margin-bottom: 16px;
  font-size: 1.5em;
}

.legal-content h1 {
  margin-bottom: 24px;
}

.legal-content p {
  margin-bottom: 16px;
}

.legal-content ul {
  margin-left: 24px;
  margin-bottom: 16px;
}

.legal-content li {
  margin-bottom: 8px;
}

.legal-content a {
  color: var(--n-primary-color);
  text-decoration: none;
}

.legal-content a:hover {
  text-decoration: underline;
}
</style>
