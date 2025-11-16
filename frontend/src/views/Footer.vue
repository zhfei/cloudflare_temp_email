<script setup>
import { useI18n } from 'vue-i18n'
import { useGlobalState } from '../store'
import { getRouterPathWithLang } from '../utils'

const { openSettings } = useGlobalState()
const { locale } = useI18n()

const { t } = useI18n({
    messages: {
        en: {
            copyright: "Copyright",
            privacyPolicy: 'Privacy Policy',
            termsOfService: 'Terms of Service',
            aboutUs: 'About Us'
        },
        zh: {
            copyright: "版权所有",
            privacyPolicy: '隐私政策',
            termsOfService: '服务条款',
            aboutUs: '关于我们'
        }
    }
});
</script>

<template>
    <div>
        <!-- 版权信息 -->
        <n-divider class="footer-divider" />
        <div style="text-align: center; padding: 20px">
            <!-- 法律链接 -->
            <n-space justify="center" style="margin-bottom: 15px;">
                <router-link :to="getRouterPathWithLang('/legal/privacy', locale)" class="footer-link">
                    {{ t('privacyPolicy') }}
                </router-link>
                <n-text depth="3">|</n-text>
                <router-link :to="getRouterPathWithLang('/legal/terms', locale)" class="footer-link">
                    {{ t('termsOfService') }}
                </router-link>
                <n-text depth="3">|</n-text>
                <router-link :to="getRouterPathWithLang('/legal/about', locale)" class="footer-link">
                    {{ t('aboutUs') }}
                </router-link>
            </n-space>
            <n-space justify="center">
                <n-text depth="3">
                    {{ t('copyright') }} © 2025-{{ new Date().getFullYear() }}
                </n-text>
                <n-text depth="3">
                    <div v-html="openSettings.copyright"></div>
                </n-text>
            </n-space>
        </div>
    </div>
</template>


<style scoped>
.footer-divider {
    margin: 0;
    padding: 0 var(--x-padding);
}

.footer-link {
    color: var(--n-text-color);
    text-decoration: none;
    transition: color 0.3s;
}

.footer-link:hover {
    color: var(--n-primary-color);
    text-decoration: underline;
}
</style>
