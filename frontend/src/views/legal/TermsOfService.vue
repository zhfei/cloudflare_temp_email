<script setup>
import { useI18n } from 'vue-i18n'
import { useHead } from '@unhead/vue'

const { locale, t } = useI18n({
  messages: {
    en: {
      title: 'Terms of Service',
      lastUpdated: 'Last Updated',
      effectiveDate: 'Effective Date'
    },
    zh: {
      title: '服务条款',
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
          <h2>1. 服务接受</h2>
          <p>通过访问和使用本网站，您同意遵守这些服务条款。如果您不同意这些条款，请不要使用本服务。</p>

          <h2>2. 服务描述</h2>
          <p>本网站提供临时邮箱服务，允许用户接收和查看发送到临时邮箱地址的邮件。本服务仅供合法用途使用。</p>

          <h2>3. 使用限制</h2>
          <p>您同意不会：</p>
          <ul>
            <li>将本服务用于任何非法目的或违反任何法律法规</li>
            <li>使用本服务发送垃圾邮件、钓鱼邮件或其他恶意内容</li>
            <li>试图破坏、干扰或损害本服务的正常运行</li>
            <li>未经授权访问本服务的任何部分</li>
            <li>冒充他人或提供虚假信息</li>
            <li>使用自动化工具过度使用本服务</li>
          </ul>

          <h2>4. 免责声明</h2>
          <p><strong>重要提示</strong>：</p>
          <ul>
            <li>本服务提供的临时邮箱地址（包括但不限于.edu域名邮箱）仅用于技术演示和教育目的。</li>
            <li>我们与任何教育机构、组织、域名注册机构或官方机构没有关联、认可或授权关系。</li>
            <li>使用.edu或其他域名邮箱地址不代表您与该域名相关的任何机构有任何关联。</li>
            <li>本服务不提供任何形式的身份验证或授权。</li>
            <li>请勿使用本服务进行任何可能误导他人的活动。</li>
          </ul>

          <h2>5. 服务可用性</h2>
          <p>我们努力保持服务的持续可用性，但不保证服务不会中断、无错误或完全安全。我们保留随时修改、暂停或终止服务的权利，无需事先通知。</p>

          <h2>6. 数据保留和删除</h2>
          <p>临时邮箱中的邮件会根据我们的数据保留政策自动删除。我们不对任何数据的丢失或删除承担责任。建议您不要将本服务用于存储重要信息。</p>

          <h2>7. 知识产权</h2>
          <p>本网站的所有内容，包括但不限于文本、图形、徽标、图标、图像、软件和代码，均受版权、商标和其他知识产权法保护。未经明确书面许可，您不得复制、修改、分发或使用这些内容。</p>

          <h2>8. 用户生成内容</h2>
          <p>通过使用本服务，您承认：</p>
          <ul>
            <li>您对通过本服务发送或接收的所有内容负责</li>
            <li>我们不对任何用户生成的内容承担责任</li>
            <li>我们保留删除任何我们认为不当、非法或违反这些条款的内容的权利</li>
          </ul>

          <h2>9. 隐私</h2>
          <p>您的隐私对我们很重要。请查看我们的<a href="/legal/privacy">隐私政策</a>，了解我们如何收集、使用和保护您的信息。</p>

          <h2>10. 第三方链接</h2>
          <p>本网站可能包含指向第三方网站的链接。我们不对这些网站的内容、隐私政策或做法负责。访问这些链接的风险由您自行承担。</p>

          <h2>11. 责任限制</h2>
          <p>在法律允许的最大范围内，我们不对因使用或无法使用本服务而产生的任何直接、间接、偶然、特殊或后果性损害承担责任。</p>

          <h2>12. 赔偿</h2>
          <p>您同意赔偿并使我们免受因您违反这些服务条款或使用本服务而产生的任何索赔、损失、责任和费用（包括律师费）。</p>

          <h2>13. 终止</h2>
          <p>我们保留随时终止或暂停您访问本服务的权利，无需事先通知，原因包括但不限于违反这些服务条款。</p>

          <h2>14. 适用法律</h2>
          <p>这些服务条款受适用法律管辖。任何争议应通过友好协商解决，如协商不成，应提交有管辖权的法院解决。</p>

          <h2>15. 条款修改</h2>
          <p>我们保留随时修改这些服务条款的权利。重大变更将在网站上发布通知。继续使用本服务即表示您接受修改后的条款。</p>

          <h2>16. 联系我们</h2>
          <p>如果您对这些服务条款有任何问题，请通过网站上的"联系我们"页面或管理员邮箱（如已配置）与我们联系。</p>
        </template>

        <template v-else>
          <h2>1. Acceptance of Terms</h2>
          <p>By accessing and using this website, you agree to comply with these Terms of Service. If you do not agree to these terms, please do not use this service.</p>

          <h2>2. Service Description</h2>
          <p>This website provides temporary email services that allow users to receive and view emails sent to temporary email addresses. This service is for lawful purposes only.</p>

          <h2>3. Use Restrictions</h2>
          <p>You agree not to:</p>
          <ul>
            <li>Use this service for any illegal purpose or in violation of any laws or regulations</li>
            <li>Use this service to send spam, phishing emails, or other malicious content</li>
            <li>Attempt to disrupt, interfere with, or damage the normal operation of this service</li>
            <li>Access any part of this service without authorization</li>
            <li>Impersonate others or provide false information</li>
            <li>Use automated tools to excessively use this service</li>
          </ul>

          <h2>4. Disclaimer</h2>
          <p><strong>Important Notice</strong>:</p>
          <ul>
            <li>The temporary email addresses provided by this service (including but not limited to .edu domain emails) are for technical demonstration and educational purposes only.</li>
            <li>We are not affiliated with, endorsed by, or authorized by any educational institutions, organizations, domain registrars, or official agencies.</li>
            <li>Using .edu or other domain email addresses does not represent any association with any institution related to that domain.</li>
            <li>This service does not provide any form of identity verification or authorization.</li>
            <li>Do not use this service for any activities that may mislead others.</li>
          </ul>

          <h2>5. Service Availability</h2>
          <p>We strive to maintain continuous service availability but do not guarantee that the service will be uninterrupted, error-free, or completely secure. We reserve the right to modify, suspend, or terminate the service at any time without prior notice.</p>

          <h2>6. Data Retention and Deletion</h2>
          <p>Emails in temporary mailboxes are automatically deleted according to our data retention policy. We are not responsible for any loss or deletion of data. We recommend that you do not use this service to store important information.</p>

          <h2>7. Intellectual Property</h2>
          <p>All content on this website, including but not limited to text, graphics, logos, icons, images, software, and code, is protected by copyright, trademark, and other intellectual property laws. You may not copy, modify, distribute, or use this content without explicit written permission.</p>

          <h2>8. User-Generated Content</h2>
          <p>By using this service, you acknowledge that:</p>
          <ul>
            <li>You are responsible for all content sent or received through this service</li>
            <li>We are not responsible for any user-generated content</li>
            <li>We reserve the right to delete any content we deem inappropriate, illegal, or in violation of these terms</li>
          </ul>

          <h2>9. Privacy</h2>
          <p>Your privacy is important to us. Please review our <a href="/legal/privacy">Privacy Policy</a> to understand how we collect, use, and protect your information.</p>

          <h2>10. Third-Party Links</h2>
          <p>This website may contain links to third-party websites. We are not responsible for the content, privacy policies, or practices of these websites. You access these links at your own risk.</p>

          <h2>11. Limitation of Liability</h2>
          <p>To the maximum extent permitted by law, we are not liable for any direct, indirect, incidental, special, or consequential damages arising from the use or inability to use this service.</p>

          <h2>12. Indemnification</h2>
          <p>You agree to indemnify and hold us harmless from any claims, losses, liabilities, and expenses (including attorney fees) arising from your violation of these Terms of Service or use of this service.</p>

          <h2>13. Termination</h2>
          <p>We reserve the right to terminate or suspend your access to this service at any time without prior notice, for reasons including but not limited to violation of these Terms of Service.</p>

          <h2>14. Governing Law</h2>
          <p>These Terms of Service are governed by applicable law. Any disputes shall be resolved through friendly negotiation, and if negotiation fails, shall be submitted to a court with jurisdiction.</p>

          <h2>15. Modification of Terms</h2>
          <p>We reserve the right to modify these Terms of Service at any time. Significant changes will be notified on the website. Continued use of this service indicates acceptance of the modified terms.</p>

          <h2>16. Contact Us</h2>
          <p>If you have any questions about these Terms of Service, please contact us through the "Contact Us" page on the website or the administrator email (if configured).</p>
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
