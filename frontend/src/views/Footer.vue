<script setup>
import { useI18n } from 'vue-i18n'
import { useRouter } from 'vue-router'
import { useGlobalState } from '../store'
import { getRouterPathWithLang } from '../utils'

const { openSettings } = useGlobalState()
const router = useRouter()

const { locale, t } = useI18n({
    messages: {
        en: {
            copyright: "Copyright",
            privacyPolicy: "Privacy Policy",
            termsOfService: "Terms of Service",
            blog: "Blog",
            resources: "Resources",
            about: "About"
        },
        zh: {
            copyright: "版权所有",
            privacyPolicy: "隐私政策",
            termsOfService: "服务条款",
            blog: "博客",
            resources: "资源中心",
            about: "关于"
        }
    }
});

const goToPage = (path) => {
    router.push(getRouterPathWithLang(path, locale.value))
}

</script>

<template>
    <div>
        <n-divider class="footer-divider" />
        <div style="padding: 20px">
            <!-- 链接导航 -->
            <n-space justify="center" style="margin-bottom: 16px;" wrap>
                <n-button text size="small" @click="goToPage('/blog')">
                    {{ t('blog') }}
                </n-button>
                <n-button text size="small" @click="goToPage('/resources')">
                    {{ t('resources') }}
                </n-button>
                <n-button text size="small" @click="goToPage('/legal/privacy')">
                    {{ t('privacyPolicy') }}
                </n-button>
                <n-button text size="small" @click="goToPage('/legal/terms')">
                    {{ t('termsOfService') }}
                </n-button>
                <n-button text size="small" @click="goToPage('/')">
                    {{ t('about') }}
                </n-button>
            </n-space>
            
            <!-- 版权信息 -->
            <div style="text-align: center;">
                <n-space justify="center">
                    <n-text depth="3">
                        {{ t('copyright') }} © 2023-{{ new Date().getFullYear() }}
                    </n-text>
                    <n-text depth="3">
                        <div v-html="openSettings.copyright"></div>
                    </n-text>
                </n-space>
            </div>
        </div>
    </div>
</template>


<style scoped>
.footer-divider {
    margin: 0;
    padding: 0 var(--x-padding);
}
</style>
