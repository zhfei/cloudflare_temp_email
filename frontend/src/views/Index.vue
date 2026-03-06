<script setup>
import { defineAsyncComponent, onMounted, watch } from 'vue'
import { useI18n } from 'vue-i18n'
import { useRoute } from 'vue-router'

import { useGlobalState } from '../store'
import { api } from '../api'
import { getRouterPathWithLang } from '../utils'

import AddressBar from './index/AddressBar.vue';
import MailBox from '../components/MailBox.vue';
import SendBox from '../components/SendBox.vue';
import AutoReply from './index/AutoReply.vue';
import AccountSettings from './index/AccountSettings.vue';
import Appearance from './common/Appearance.vue';
import Webhook from './index/Webhook.vue';
import Attachment from './index/Attachment.vue';
import About from './common/About.vue';
import AdsterraNativeBanner from '../components/AdsterraNativeBanner.vue';

import SimpleIndex from './index/SimpleIndex.vue';

const { loading, settings, openSettings, indexTab, globalTabplacement, useSimpleIndex } = useGlobalState()
const message = useMessage()
const route = useRoute()
const { locale } = useI18n()

const SendMail = defineAsyncComponent(() => {
  loading.value = true;
  return import('./index/SendMail.vue')
    .finally(() => loading.value = false);
});

const { t } = useI18n({
  messages: {
    en: {
      mailbox: 'Mail Box',
      sendbox: 'Send Box',
      sendmail: 'Send Mail',
      auto_reply: 'Auto Reply',
      accountSettings: 'Account Settings',
      appearance: 'Appearance',
      about: 'About',
      s3Attachment: 'S3 Attachment',
      saveToS3Success: 'save to s3 success',
      webhookSettings: 'Webhook Settings',
      query: 'Query',
      disclaimerTitle: 'Important Disclaimer',
      disclaimerText: 'This service is a third-party temporary email tool and is not affiliated with any educational institutions. Any .edu email addresses provided are temporary and for educational/testing purposes only. We are not responsible for any misuse of these addresses. Please use this service responsibly and in compliance with applicable laws and regulations.',
      readTerms: 'Read Terms of Service'
    },
    zh: {
      mailbox: '收件箱',
      disclaimerTitle: '重要免责声明',
      disclaimerText: '本服务是第三方临时邮箱工具，与任何教育机构无关。提供的任何 .edu 邮箱地址都是临时的，仅用于教育/测试目的。我们不对这些地址的任何滥用行为负责。请负责任地使用本服务，并遵守适用的法律法规。',
      readTerms: '阅读服务条款',
      sendbox: '发件箱',
      sendmail: '发送邮件',
      auto_reply: '自动回复',
      accountSettings: '账户',
      appearance: '外观',
      about: '关于',
      s3Attachment: 'S3附件',
      saveToS3Success: '保存到s3成功',
      webhookSettings: 'Webhook 设置',
      query: '查询',
    }
  }
});

const fetchMailData = async (limit, offset) => {
  if (mailIdQuery.value > 0) {
    const singleMail = await api.fetch(`/api/mail/${mailIdQuery.value}`);
    if (singleMail) return { results: [singleMail], count: 1 };
    return { results: [], count: 0 };
  }
  return await api.fetch(`/api/mails?limit=${limit}&offset=${offset}`);
};

const deleteMail = async (curMailId) => {
  await api.fetch(`/api/mails/${curMailId}`, { method: 'DELETE' });
};

const deleteSenboxMail = async (curMailId) => {
  await api.fetch(`/api/sendbox/${curMailId}`, { method: 'DELETE' });
};

const fetchSenboxData = async (limit, offset) => {
  return await api.fetch(`/api/sendbox?limit=${limit}&offset=${offset}`);
};

const saveToS3 = async (mail_id, filename, blob) => {
  try {
    const { url } = await api.fetch(`/api/attachment/put_url`, {
      method: 'POST',
      body: JSON.stringify({ key: `${mail_id}/${filename}` })
    });
    // upload to s3 by formdata
    const formData = new FormData();
    formData.append(filename, blob);
    await fetch(url, {
      method: 'PUT',
      body: formData
    });
    message.success(t('saveToS3Success'));
  } catch (error) {
    console.error(error);
    message.error(error.message || "save to s3 error");
  }
}

const mailBoxKey = ref("")
const mailIdQuery = ref("")
const showMailIdQuery = ref(false)

const queryMail = () => {
  mailBoxKey.value = Date.now();
}

watch(route, () => {
  if (!route.query.mail_id) {
    showMailIdQuery.value = false;
    mailIdQuery.value = "";
    queryMail();
  }
})

onMounted(() => {
  if (route.query.mail_id) {
    showMailIdQuery.value = true;
    mailIdQuery.value = route.query.mail_id;
    queryMail();
  }
})
</script>

<template>
  <div>
    <div v-if="useSimpleIndex">
      <SimpleIndex />
    </div>
    <div v-else>
      <!-- 免责声明 -->
      <n-card :bordered="false" embedded style="margin-bottom: 10px;">
        <n-alert type="warning" :show-icon="true" :bordered="true">
          <template #header>
            <strong>{{ t('disclaimerTitle') }}</strong>
          </template>
          <p>{{ t('disclaimerText') }}</p>
          <p style="margin-top: 10px;">
            <router-link :to="getRouterPathWithLang('/legal/terms', locale)" style="color: var(--n-warning-color);">
              {{ t('readTerms') }}
            </router-link>
          </p>
        </n-alert>
      </n-card>
      <AddressBar />
      <AdsterraNativeBanner />
      <n-tabs v-if="settings.address" type="card" v-model:value="indexTab" :placement="globalTabplacement">
        <n-tab-pane name="mailbox" :tab="t('mailbox')">
          <div v-if="showMailIdQuery" style="margin-bottom: 10px;">
            <n-input-group>
              <n-input v-model:value="mailIdQuery" />
              <n-button @click="queryMail" type="primary" tertiary>
                {{ t('query') }}
              </n-button>
            </n-input-group>
          </div>
          <MailBox :key="mailBoxKey" :showEMailTo="false" :showReply="true" :showSaveS3="openSettings.isS3Enabled"
            :saveToS3="saveToS3" :enableUserDeleteEmail="openSettings.enableUserDeleteEmail"
            :fetchMailData="fetchMailData" :deleteMail="deleteMail" />
        </n-tab-pane>
        <n-tab-pane name="sendbox" :tab="t('sendbox')">
          <SendBox :fetchMailData="fetchSenboxData" :enableUserDeleteEmail="openSettings.enableUserDeleteEmail"
            :deleteMail="deleteSenboxMail" />
        </n-tab-pane>
        <n-tab-pane name="sendmail" :tab="t('sendmail')">
          <SendMail />
        </n-tab-pane>
        <n-tab-pane name="accountSettings" :tab="t('accountSettings')">
          <AccountSettings />
        </n-tab-pane>
        <n-tab-pane name="appearance" :tab="t('appearance')">
          <Appearance :showUseSimpleIndex="true" />
        </n-tab-pane>
        <n-tab-pane v-if="openSettings.enableAutoReply" name="auto_reply" :tab="t('auto_reply')">
          <AutoReply />
        </n-tab-pane>
        <n-tab-pane v-if="openSettings.enableWebhook" name="webhook" :tab="t('webhookSettings')">
          <Webhook />
        </n-tab-pane>
        <n-tab-pane v-if="openSettings.isS3Enabled" name="s3_attachment" :tab="t('s3Attachment')">
          <Attachment />
        </n-tab-pane>
        <n-tab-pane v-if="openSettings.enableIndexAbout" name="about" :tab="t('about')">
          <About />
        </n-tab-pane>
      </n-tabs>
    </div>
  </div>
</template>
