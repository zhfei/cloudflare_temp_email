<script setup>
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
import { useGlobalState } from '../store'
import { 
  SchoolFilled, 
  CodeFilled, 
  CloudFilled, 
  StorageFilled,
  SecurityFilled
} from '@vicons/material'

const { openSettings } = useGlobalState()

const { t } = useI18n({
    messages: {
        en: {
            copyright: "Copyright",
            studentDiscounts: 'Education Discounts',
            studentDiscountsDesc: 'Exclusive discounts and free resources for education',
            developmentTools: 'Development Tools',
            cloudServices: 'Cloud Services',
            designTools: 'Design Tools',
            productivityTools: 'Productivity Tools',
            learningResources: 'Learning Resources',
            musicAndVideo: 'Music & Video',
            businessTools: 'Business Tools',
            securityTools: 'Security Tools',
            storageAndBackup: 'Storage & Backup',
            researchAndAcademic: 'Research & Academic',
            viewDetails: 'View Details',
            free: 'Free',
            discount: 'Discount',
            limited: 'Limited Time',
            verified: 'Verified',
            unverified: 'Unverified'
        },
        zh: {
            copyright: "版权所有",
            studentDiscounts: '教育优惠',
            studentDiscountsDesc: '教育专属折扣和免费资源',
            developmentTools: '开发工具',
            cloudServices: '云服务',
            designTools: '设计工具',
            productivityTools: '生产力工具',
            learningResources: '学习资源',
            musicAndVideo: '音乐视频',
            businessTools: '商业工具',
            securityTools: '安全工具',
            storageAndBackup: '存储备份',
            researchAndAcademic: '研究学术',
            viewDetails: '查看详情',
            free: '免费',
            discount: '折扣',
            limited: '限时',
            verified: '已验证',
            unverified: '未验证'
        }
    }
});

// 教育优惠数据 - 基于 GitHub Student-resources
const studentDiscounts = ref([
  {
    category: 'developmentTools',
    items: [
      {
        name: 'GitHub Student Developer Pack',
        description: 'Free access to developer tools and services',
        discount: 'Free',
        status: 'verified',
        url: 'https://education.github.com/pack',
        icon: CodeFilled,
        features: ['GitHub Pro', 'JetBrains IDEs', 'DigitalOcean Credits', 'AWS Credits']
      },
      {
        name: 'JetBrains All Products Pack',
        description: 'Professional development tools for students',
        discount: 'Free',
        status: 'verified',
        url: 'https://www.jetbrains.com/community/education/',
        icon: CodeFilled,
        features: ['IntelliJ IDEA', 'PyCharm', 'WebStorm', 'DataGrip']
      },
      {
        name: 'Microsoft Azure for Students',
        description: 'Free Azure credits and services',
        discount: '$100 Credits',
        status: 'verified',
        url: 'https://azure.microsoft.com/en-us/free/students/',
        icon: CloudFilled,
        features: ['Virtual Machines', 'App Services', 'Databases', 'AI Services']
      }
    ]
  },
  {
    category: 'cloudServices',
    items: [
      {
        name: 'AWS Educate',
        description: 'Free AWS credits and learning resources',
        discount: '$100 Credits',
        status: 'verified',
        url: 'https://aws.amazon.com/education/awseducate/',
        icon: CloudFilled,
        features: ['EC2', 'S3', 'Lambda', 'CloudFormation']
      },
      {
        name: 'Google Cloud Platform',
        description: 'Free credits for students',
        discount: '$50 Credits',
        status: 'verified',
        url: 'https://cloud.google.com/edu/',
        icon: CloudFilled,
        features: ['Compute Engine', 'Cloud Storage', 'BigQuery', 'AI Platform']
      },
      {
        name: 'DigitalOcean',
        description: 'Free credits for GitHub Student Pack members',
        discount: '$50 Credits',
        status: 'verified',
        url: 'https://www.digitalocean.com/',
        icon: CloudFilled,
        features: ['Droplets', 'Spaces', 'Databases', 'Kubernetes']
      }
    ]
  },
  {
    category: 'designTools',
    items: [
      {
        name: 'Adobe Creative Cloud',
        description: 'Complete creative software suite',
        discount: '60% Off',
        status: 'verified',
        url: 'https://www.adobe.com/creativecloud/plans.html',
        icon: SchoolFilled,
        features: ['Photoshop', 'Illustrator', 'Premiere Pro', 'After Effects']
      },
      {
        name: 'Figma',
        description: 'Collaborative design tool',
        discount: 'Free Pro',
        status: 'verified',
        url: 'https://www.figma.com/education/',
        icon: SchoolFilled,
        features: ['Unlimited Projects', 'Team Collaboration', 'Advanced Features']
      },
      {
        name: 'Sketch',
        description: 'Professional design tool for Mac',
        discount: '50% Off',
        status: 'verified',
        url: 'https://www.sketch.com/education/',
        icon: SchoolFilled,
        features: ['Design Tools', 'Prototyping', 'Developer Handoff']
      }
    ]
  },
  {
    category: 'productivityTools',
    items: [
      {
        name: 'Microsoft Office 365',
        description: 'Complete office suite for students',
        discount: 'Free',
        status: 'verified',
        url: 'https://www.microsoft.com/en-us/education/products/office',
        icon: SchoolFilled,
        features: ['Word', 'Excel', 'PowerPoint', 'OneDrive']
      },
      {
        name: 'Notion',
        description: 'All-in-one workspace',
        discount: 'Free Pro',
        status: 'verified',
        url: 'https://www.notion.so/students',
        icon: SchoolFilled,
        features: ['Unlimited Blocks', 'Version History', 'Advanced Sharing']
      },
      {
        name: 'Grammarly Premium',
        description: 'Advanced writing assistant',
        discount: 'Free',
        status: 'verified',
        url: 'https://www.grammarly.com/education',
        icon: SchoolFilled,
        features: ['Advanced Grammar', 'Style Suggestions', 'Plagiarism Detection']
      }
    ]
  },
  {
    category: 'learningResources',
    items: [
      {
        name: 'Coursera',
        description: 'Online courses from top universities',
        discount: 'Free Courses',
        status: 'verified',
        url: 'https://www.coursera.org/',
        icon: SchoolFilled,
        features: ['Free Courses', 'Certificates', 'Specializations', 'Degrees']
      },
      {
        name: 'Udemy',
        description: 'Online learning platform',
        discount: 'Up to 90% Off',
        status: 'verified',
        url: 'https://www.udemy.com/',
        icon: SchoolFilled,
        features: ['Development', 'Design', 'Business', 'Marketing']
      },
      {
        name: 'Pluralsight',
        description: 'Technology skills platform',
        discount: 'Free',
        status: 'verified',
        url: 'https://www.pluralsight.com/',
        icon: SchoolFilled,
        features: ['Tech Skills', 'Certification Prep', 'Hands-on Labs']
      }
    ]
  },
  {
    category: 'musicAndVideo',
    items: [
      {
        name: 'Spotify Premium',
        description: 'Ad-free music streaming',
        discount: '50% Off',
        status: 'verified',
        url: 'https://www.spotify.com/us/student/',
        icon: SchoolFilled,
        features: ['Ad-free Music', 'Offline Downloads', 'High Quality Audio']
      },
      {
        name: 'YouTube Premium',
        description: 'Ad-free video streaming',
        discount: '50% Off',
        status: 'verified',
        url: 'https://www.youtube.com/premium/student',
        icon: SchoolFilled,
        features: ['Ad-free Videos', 'Background Play', 'YouTube Music']
      },
      {
        name: 'Apple Music',
        description: 'Music streaming service',
        discount: '50% Off',
        status: 'verified',
        url: 'https://www.apple.com/apple-music/',
        icon: SchoolFilled,
        features: ['Ad-free Music', 'Spatial Audio', 'Lyrics']
      }
    ]
  },
  {
    category: 'securityTools',
    items: [
      {
        name: '1Password',
        description: 'Password manager',
        discount: 'Free',
        status: 'verified',
        url: 'https://1password.com/students/',
        icon: SecurityFilled,
        features: ['Password Generation', 'Secure Sharing', 'Two-Factor Auth']
      },
      {
        name: 'Dashlane',
        description: 'Password manager and VPN',
        discount: 'Free',
        status: 'verified',
        url: 'https://www.dashlane.com/students',
        icon: SecurityFilled,
        features: ['Password Manager', 'VPN Service', 'Dark Web Monitoring']
      }
    ]
  },
  {
    category: 'storageAndBackup',
    items: [
      {
        name: 'Dropbox',
        description: 'Cloud storage and file sharing',
        discount: '50% Off',
        status: 'verified',
        url: 'https://www.dropbox.com/education',
        icon: StorageFilled,
        features: ['2TB Storage', 'File Sharing', 'Version History', 'Mobile Access']
      },
      {
        name: 'Google Drive',
        description: 'Cloud storage with Google Workspace',
        discount: 'Free',
        status: 'verified',
        url: 'https://edu.google.com/products/workspace-for-education/',
        icon: StorageFilled,
        features: ['Unlimited Storage', 'Google Docs', 'Sheets', 'Slides']
      },
      {
        name: 'OneDrive',
        description: 'Microsoft cloud storage',
        discount: 'Free',
        status: 'verified',
        url: 'https://www.microsoft.com/en-us/education/products/office',
        icon: StorageFilled,
        features: ['1TB Storage', 'Office Online', 'File Sharing', 'Mobile Apps']
      }
    ]
  },
  {
    category: 'researchAndAcademic',
    items: [
      {
        name: 'Mendeley',
        description: 'Reference manager and academic social network',
        discount: 'Free',
        status: 'verified',
        url: 'https://www.mendeley.com/',
        icon: SchoolFilled,
        features: ['Reference Management', 'PDF Annotation', 'Citation Tools', 'Academic Network']
      },
      {
        name: 'Zotero',
        description: 'Free reference manager',
        discount: 'Free',
        status: 'verified',
        url: 'https://www.zotero.org/',
        icon: SchoolFilled,
        features: ['Reference Collection', 'Citation Generation', 'PDF Storage', 'Browser Integration']
      },
      {
        name: 'Overleaf',
        description: 'Online LaTeX editor',
        discount: 'Free Pro',
        status: 'verified',
        url: 'https://www.overleaf.com/edu',
        icon: SchoolFilled,
        features: ['LaTeX Editor', 'Real-time Collaboration', 'Templates', 'Version Control']
      }
    ]
  }
])

const getCategoryName = (category) => {
  return t(category)
}

const getStatusColor = (status) => {
  return status === 'verified' ? 'success' : 'warning'
}

const getStatusText = (status) => {
  return t(status)
}

const getDiscountColor = (discount) => {
  if (discount.toLowerCase().includes('free')) return 'success'
  if (discount.toLowerCase().includes('off')) return 'warning'
  return 'info'
}

const openUrl = (url) => {
  if (url) {
    window.open(url, '_blank', 'noopener,noreferrer')
  }
}
</script>

<template>
    <div>
        <!-- 教育优惠组件 -->
        <div class="education-discounts-section">
            <n-card :bordered="false" embedded>
                <template #header>
                    <div class="header">
                        <n-icon :component="SchoolFilled" size="24" />
                        <span class="title">{{ t('studentDiscounts') }}</span>
                    </div>
                </template>
                
                <n-space vertical size="large">
                    <p class="description">{{ t('studentDiscountsDesc') }}</p>
                    
                    <n-collapse accordion>
                        <n-collapse-item 
                            v-for="category in studentDiscounts" 
                            :key="category.category"
                            :name="category.category"
                            :title="getCategoryName(category.category)"
                        >
                            <n-grid :cols="1" :x-gap="12" :y-gap="12">
                                <n-gi v-for="item in category.items" :key="item.name">
                                    <n-card :bordered="false" embedded class="discount-item">
                                        <div class="item-header">
                                            <div class="item-info">
                                                <n-icon :component="item.icon" size="20" />
                                                <div class="item-details">
                                                    <h4 class="item-name">{{ item.name }}</h4>
                                                    <p class="item-description">{{ item.description }}</p>
                                                </div>
                                            </div>
                                            <div class="item-badges">
                                                <n-tag :type="getDiscountColor(item.discount)" size="small">
                                                    {{ item.discount }}
                                                </n-tag>
                                                <n-tag :type="getStatusColor(item.status)" size="small">
                                                    {{ getStatusText(item.status) }}
                                                </n-tag>
                                            </div>
                                        </div>
                                        
                                        <div class="item-features">
                                            <n-tag 
                                                v-for="feature in item.features" 
                                                :key="feature"
                                                type="info" 
                                                size="small"
                                                class="feature-tag"
                                            >
                                                {{ feature }}
                                            </n-tag>
                                        </div>
                                        
                                        <div class="item-actions">
                                            <n-button 
                                                type="primary" 
                                                size="small" 
                                                @click="openUrl(item.url)"
                                            >
                                                {{ t('viewDetails') }}
                                            </n-button>
                                        </div>
                                    </n-card>
                                </n-gi>
                            </n-grid>
                        </n-collapse-item>
                    </n-collapse>
                </n-space>
            </n-card>
        </div>

        <!-- 版权信息 -->
        <n-divider class="footer-divider" />
        <div style="text-align: center; padding: 20px">
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
.education-discounts-section {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.header {
  display: flex;
  align-items: center;
  gap: 8px;
}

.title {
  font-size: 18px;
  font-weight: 600;
}

.description {
  color: #666;
  margin: 0;
  text-align: center;
}

.discount-item {
  transition: all 0.3s ease;
}

.discount-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.item-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 12px;
}

.item-info {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  flex: 1;
}

.item-details {
  flex: 1;
}

.item-name {
  margin: 0 0 4px 0;
  font-size: 16px;
  font-weight: 600;
}

.item-description {
  margin: 0;
  color: #666;
  font-size: 14px;
}

.item-badges {
  display: flex;
  gap: 8px;
  flex-shrink: 0;
}

.item-features {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 12px;
}

.feature-tag {
  font-size: 12px;
}

.item-actions {
  display: flex;
  justify-content: flex-end;
}

.footer-divider {
    margin: 0;
    padding: 0 var(--x-padding);
}

@media (max-width: 768px) {
  .item-header {
    flex-direction: column;
    gap: 12px;
  }
  
  .item-badges {
    align-self: flex-start;
  }
  
  .item-actions {
    justify-content: flex-start;
  }
}
</style>
