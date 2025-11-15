<template>
  <div class="legal-page">
    <n-card>
      <template #header>
        <h1>{{ t('termsOfService') }}</h1>
        <n-text depth="3">{{ t('lastUpdated') }}: {{ lastUpdated }}</n-text>
      </template>

      <n-space vertical size="large">
        <section>
          <h2>{{ t('acceptance') }}</h2>
          <p>{{ t('acceptanceDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('serviceDescription') }}</h2>
          <p>{{ t('serviceDesc') }}</p>
          <p><strong>{{ t('importantNotice') }}</strong></p>
          <n-alert type="warning" :show-icon="true">
            {{ t('eduDisclaimer') }}
          </n-alert>
        </section>

        <section>
          <h2>{{ t('userObligations') }}</h2>
          <p>{{ t('userObligationsDesc') }}</p>
          <ul>
            <li>{{ t('obligation1') }}</li>
            <li>{{ t('obligation2') }}</li>
            <li>{{ t('obligation3') }}</li>
            <li>{{ t('obligation4') }}</li>
            <li>{{ t('obligation5') }}</li>
          </ul>
        </section>

        <section>
          <h2>{{ t('prohibitedUses') }}</h2>
          <p>{{ t('prohibitedDesc') }}</p>
          <ul>
            <li>{{ t('prohibited1') }}</li>
            <li>{{ t('prohibited2') }}</li>
            <li>{{ t('prohibited3') }}</li>
            <li>{{ t('prohibited4') }}</li>
            <li>{{ t('prohibited5') }}</li>
            <li>{{ t('prohibited6') }}</li>
          </ul>
        </section>

        <section>
          <h2>{{ t('intellectualProperty') }}</h2>
          <p>{{ t('ipDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('disclaimers') }}</h2>
          <p>{{ t('disclaimerDesc') }}</p>
          <ul>
            <li>{{ t('disclaimer1') }}</li>
            <li>{{ t('disclaimer2') }}</li>
            <li>{{ t('disclaimer3') }}</li>
          </ul>
        </section>

        <section>
          <h2>{{ t('limitationOfLiability') }}</h2>
          <p>{{ t('liabilityDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('termination') }}</h2>
          <p>{{ t('terminationDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('changesToTerms') }}</h2>
          <p>{{ t('termsChangesDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('governingLaw') }}</h2>
          <p>{{ t('governingLawDesc') }}</p>
        </section>

        <section>
          <h2>{{ t('contactInformation') }}</h2>
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
      termsOfService: 'Terms of Service',
      lastUpdated: 'Last Updated',
      acceptance: '1. Acceptance of Terms',
      acceptanceDesc: 'By accessing and using this service, you accept and agree to be bound by the terms and provision of this agreement.',
      
      serviceDescription: '2. Service Description',
      serviceDesc: 'We provide a temporary email service that allows users to create temporary email addresses for receiving emails. This service is provided "as is" without warranties of any kind.',
      importantNotice: 'Important Notice:',
      eduDisclaimer: 'This service is a third-party tool and is not affiliated with any educational institutions. Any .edu email addresses provided are temporary and for educational/testing purposes only. We are not responsible for any misuse of these addresses.',
      
      userObligations: '3. User Obligations',
      userObligationsDesc: 'Users agree to:',
      obligation1: 'Use the service only for lawful purposes',
      obligation2: 'Not use the service to send spam or malicious content',
      obligation3: 'Not impersonate others or provide false information',
      obligation4: 'Respect the privacy and rights of others',
      obligation5: 'Comply with all applicable laws and regulations',
      
      prohibitedUses: '4. Prohibited Uses',
      prohibitedDesc: 'You may not use our service:',
      prohibited1: 'For any illegal or unauthorized purpose',
      prohibited2: 'To send spam, phishing emails, or malicious content',
      prohibited3: 'To impersonate any person or entity',
      prohibited4: 'To violate any applicable laws or regulations',
      prohibited5: 'To interfere with or disrupt the service',
      prohibited6: 'To attempt to gain unauthorized access to any part of the service',
      
      intellectualProperty: '5. Intellectual Property',
      ipDesc: 'All content, features, and functionality of the service are owned by us and are protected by international copyright, trademark, and other intellectual property laws.',
      
      disclaimers: '6. Disclaimers',
      disclaimerDesc: 'The service is provided on an "as is" and "as available" basis. We make no warranties:',
      disclaimer1: 'That the service will be uninterrupted or error-free',
      disclaimer2: 'That emails will be delivered or received reliably',
      disclaimer3: 'Regarding the security or privacy of emails transmitted through the service',
      
      limitationOfLiability: '7. Limitation of Liability',
      liabilityDesc: 'To the maximum extent permitted by law, we shall not be liable for any indirect, incidental, special, consequential, or punitive damages resulting from your use of the service.',
      
      termination: '8. Termination',
      terminationDesc: 'We reserve the right to terminate or suspend your access to the service at any time, without prior notice, for any reason, including violation of these terms.',
      
      changesToTerms: '9. Changes to Terms',
      termsChangesDesc: 'We reserve the right to modify these terms at any time. Your continued use of the service after any changes constitutes acceptance of the new terms.',
      
      governingLaw: '10. Governing Law',
      governingLawDesc: 'These terms shall be governed by and construed in accordance with applicable laws, without regard to conflict of law provisions.',
      
      contactInformation: '11. Contact Information',
      contactDesc: 'If you have any questions about these Terms of Service, please contact us:',
      email: 'Email'
    },
    zh: {
      termsOfService: '服务条款',
      lastUpdated: '最后更新',
      acceptance: '1. 接受条款',
      acceptanceDesc: '通过访问和使用本服务，您接受并同意受本协议的条款和规定约束。',
      
      serviceDescription: '2. 服务说明',
      serviceDesc: '我们提供临时邮箱服务，允许用户创建临时邮箱地址以接收邮件。本服务按"现状"提供，不提供任何形式的保证。',
      importantNotice: '重要提示：',
      eduDisclaimer: '本服务是第三方工具，与任何教育机构无关。提供的任何 .edu 邮箱地址都是临时的，仅用于教育/测试目的。我们不对这些地址的任何滥用行为负责。',
      
      userObligations: '3. 用户义务',
      userObligationsDesc: '用户同意：',
      obligation1: '仅将服务用于合法目的',
      obligation2: '不使用服务发送垃圾邮件或恶意内容',
      obligation3: '不冒充他人或提供虚假信息',
      obligation4: '尊重他人的隐私和权利',
      obligation5: '遵守所有适用的法律法规',
      
      prohibitedUses: '4. 禁止用途',
      prohibitedDesc: '您不得使用我们的服务：',
      prohibited1: '用于任何非法或未经授权的目的',
      prohibited2: '发送垃圾邮件、钓鱼邮件或恶意内容',
      prohibited3: '冒充任何个人或实体',
      prohibited4: '违反任何适用的法律法规',
      prohibited5: '干扰或破坏服务',
      prohibited6: '试图未经授权访问服务的任何部分',
      
      intellectualProperty: '5. 知识产权',
      ipDesc: '服务的所有内容、功能和特性均归我们所有，并受国际版权、商标和其他知识产权法保护。',
      
      disclaimers: '6. 免责声明',
      disclaimerDesc: '服务按"现状"和"可用"基础提供。我们不提供任何保证：',
      disclaimer1: '服务将不间断或无错误',
      disclaimer2: '邮件将可靠地传递或接收',
      disclaimer3: '关于通过服务传输的邮件的安全性或隐私性',
      
      limitationOfLiability: '7. 责任限制',
      liabilityDesc: '在法律允许的最大范围内，我们不对因您使用服务而产生的任何间接、偶然、特殊、后果性或惩罚性损害承担责任。',
      
      termination: '8. 终止',
      terminationDesc: '我们保留随时终止或暂停您访问服务的权利，无需事先通知，包括违反这些条款的情况。',
      
      changesToTerms: '9. 条款变更',
      termsChangesDesc: '我们保留随时修改这些条款的权利。您在任何变更后继续使用服务即表示接受新条款。',
      
      governingLaw: '10. 适用法律',
      governingLawDesc: '这些条款应受适用法律管辖并根据适用法律解释，不考虑法律冲突条款。',
      
      contactInformation: '11. 联系信息',
      contactDesc: '如果您对这些服务条款有任何疑问，请联系我们：',
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
