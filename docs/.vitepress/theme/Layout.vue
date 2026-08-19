<script setup lang="ts">
import { onMounted, onBeforeUnmount, computed, ref } from 'vue'
import DefaultTheme from 'vitepress/theme'
import { useRoute } from 'vitepress'
import AutoImageZoom from './components/AutoImageZoom.vue'
import PromoBar from './components/PromoBar.vue'
import ExtensionsMegaMenu from './components/ExtensionsMegaMenu.vue'
import NavIconsMore from './components/NavIconsMore.vue'

const { Layout } = DefaultTheme
const route = useRoute()
const isHome = computed(() => route.path === '/')
const mobileExtOpen = ref(false)

const extensions = [
  { slug: 'akeneo-migration',          label: 'Akeneo Migration'   },
  { slug: 'ai-product-feed-openai',    label: 'AI Product Feed'    },
  { slug: 'auto-sku-generator',        label: 'Auto SKU Generator' },
  { slug: 'aws-integration',           label: 'AWS Integration'    },
  { slug: 'bagisto',                   label: 'Bagisto'            },
  { slug: 'bigcommerce',               label: 'BigCommerce'        },
  { slug: 'azure-integration',         label: 'Azure Integration'  },
  { slug: 'cloudflare-r2-integration', label: 'Cloudflare R2'      },
  { slug: 'cs-cart',                   label: 'CS-Cart'            },
  { slug: 'dam',                       label: 'DAM'                },
  { slug: 'deepl',                     label: 'DeepL Translator'   },
  { slug: 'erpnext',                   label: 'ERPNext'            },
  { slug: 'google-shopping',           label: 'Google Shopping'    },
  { slug: 'job-scheduler',             label: 'Job Scheduler'      },
  { slug: 'maker-checker-workflow',    label: 'Maker Checker'      },
  { slug: 'magento2',                  label: 'Magento 2'          },
  { slug: 'odoo-erp',                  label: 'Odoo ERP'           },
  { slug: 'pdf-generator',             label: 'PDF Generator'      },
  { slug: 'prestashop',                label: 'PrestaShop'         },
  { slug: 'public-image-url',          label: 'Public Image URL'   },
  { slug: 'shopify',                   label: 'Shopify'            },
  { slug: 'supplier-data-portal',      label: 'Supplier Portal'    },
  { slug: 'woocommerce',               label: 'WooCommerce'        },
  { slug: 'woocommerce-wpml',          label: 'WooCommerce WPML'   },
]

let observer: MutationObserver | null = null

function scrollActiveTocIntoView() {
  const active = document.querySelector('.VPDocAsideOutline .outline-link.active')
  if (active && (active as HTMLElement).scrollIntoView) {
    ;(active as HTMLElement).scrollIntoView({ block: 'nearest', behavior: 'smooth' })
  }
}

onMounted(() => {
  scrollActiveTocIntoView()
  const toc = document.querySelector('.VPDocAsideOutline')
  if (toc) {
    observer = new MutationObserver(() => scrollActiveTocIntoView())
    observer.observe(toc, { subtree: true, attributes: true, attributeFilter: ['class'] })
  }
})

onBeforeUnmount(() => {
  if (observer) {
    observer.disconnect()
    observer = null
  }
})
</script>

<template>
  <Layout>
    <template #layout-top>
      <PromoBar />
    </template>

    <!-- Mobile hamburger drawer -->
    <template #nav-screen-content-before>
      <div class="mobile-menu">
        <!-- Home -->
        <a href="/" class="mobile-menu-link">Home</a>

        <!-- Extensions accordion -->
        <div class="mobile-menu-group">
          <button
            class="mobile-menu-group-btn"
            @click="mobileExtOpen = !mobileExtOpen"
            :aria-expanded="mobileExtOpen"
          >
            <span>Extensions</span>
            <span class="mobile-menu-plus" :class="{ open: mobileExtOpen }">+</span>
          </button>
          <div v-if="mobileExtOpen" class="mobile-menu-ext-grid">
            <a
              v-for="ext in extensions"
              :key="ext.slug"
              :href="`/${ext.slug}/`"
              class="mobile-ext-item"
            >
              <img
                :src="`/icons/extensions/${ext.slug}.png`"
                :alt="ext.label"
                class="mobile-ext-item-icon"
                width="22"
                height="22"
              />
              <span class="mobile-ext-item-name">{{ ext.label }}</span>
            </a>
          </div>
        </div>

        <!-- External nav links -->
        <a href="https://docs.unopim.com/" class="mobile-menu-link" target="_blank" rel="noopener noreferrer">
          <span>User Guide</span>
          <svg class="mobile-ext-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="14" height="14" aria-hidden="true">
            <path fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6M15 3h6v6M10 14 21 3"/>
          </svg>
        </a>
        <a href="https://devdocs.unopim.com/" class="mobile-menu-link" target="_blank" rel="noopener noreferrer">
          <span>Dev Doc</span>
          <svg class="mobile-ext-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="14" height="14" aria-hidden="true">
            <path fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6M15 3h6v6M10 14 21 3"/>
          </svg>
        </a>
        <a href="https://unopim.com/en/contacts/" class="mobile-menu-link" target="_blank" rel="noopener noreferrer">
          <span>Contact Us</span>
          <svg class="mobile-ext-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="14" height="14" aria-hidden="true">
            <path fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6M15 3h6v6M10 14 21 3"/>
          </svg>
        </a>
      </div>
    </template>

    <!-- Desktop: all nav links right of the search bar -->
    <template #nav-bar-content-after>
      <div class="desktop-nav">
        <a href="/" class="vp-nav-link" :class="{ active: isHome }">Home</a>
        <ExtensionsMegaMenu />
        <a href="https://docs.unopim.com/" class="vp-nav-link" target="_blank" rel="noopener noreferrer">User Guide</a>
        <a href="https://devdocs.unopim.com/" class="vp-nav-link" target="_blank" rel="noopener noreferrer">Dev Doc</a>
        <a href="https://unopim.com/en/contacts/" class="vp-nav-link" target="_blank" rel="noopener noreferrer">Contact Us</a>
      </div>
      <NavIconsMore class="nav-slot-more" />
    </template>

    <template #layout-bottom>
      <AutoImageZoom />
    </template>
  </Layout>
</template>

<style scoped>
/* ── Desktop nav wrapper ─────────────────────────────── */
.desktop-nav {
  display: inline-flex;
  align-items: center;
}

/* ── Desktop nav links ───────────────────────────────── */
.vp-nav-link {
  display: inline-flex;
  align-items: center;
  padding: 0 12px;
  height: var(--vp-nav-height);
  font-size: 14px;
  font-weight: 500;
  color: var(--vp-c-text-1);
  text-decoration: none;
  white-space: nowrap;
  transition: color 0.25s;
}

.vp-nav-link:hover,
.vp-nav-link.active {
  color: var(--vp-c-brand);
  text-decoration: none;
}

/* ── Mobile menu ─────────────────────────────────────── */
.mobile-menu {
  padding: 0 2px;
  margin-bottom: 8px;
}

/* Each row item */
.mobile-menu-link {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 0 11px;
  border-top: 1px solid var(--vp-c-divider);
  font-size: 15px;
  font-weight: 500;
  line-height: 1.25;
  color: var(--vp-c-text-1);
  text-decoration: none;
  transition: color 0.25s;
}

.mobile-menu-link:hover {
  color: var(--vp-c-brand);
}

/* Extensions accordion wrapper */
.mobile-menu-group {
  border-top: 1px solid var(--vp-c-divider);
}

.mobile-menu-group-btn {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  padding: 12px 0 11px;
  font-size: 15px;
  font-weight: 500;
  line-height: 1.25;
  font-family: inherit;
  color: var(--vp-c-text-1);
  background: transparent;
  border: none;
  cursor: pointer;
  text-align: left;
  transition: color 0.25s;
}

.mobile-menu-group-btn:hover {
  color: var(--vp-c-brand);
}

.mobile-menu-plus {
  font-size: 22px;
  font-weight: 300;
  line-height: 1;
  flex-shrink: 0;
  transition: transform 0.25s ease;
}

.mobile-menu-plus.open {
  transform: rotate(45deg);
}

/* Extensions 2-column grid inside accordion */
.mobile-menu-ext-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 2px;
  max-height: 260px;
  overflow-x: hidden;
  overflow-y: auto;
  padding-bottom: 12px;
  /* custom scrollbar */
  scrollbar-width: thin;
  scrollbar-color: var(--vp-c-divider) transparent;
}

.mobile-menu-ext-grid::-webkit-scrollbar {
  width: 4px;
}

.mobile-menu-ext-grid::-webkit-scrollbar-track {
  background: transparent;
}

.mobile-menu-ext-grid::-webkit-scrollbar-thumb {
  background: var(--vp-c-divider);
  border-radius: 4px;
}

.mobile-ext-item {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 7px 8px;
  font-size: 13px;
  font-weight: 500;
  color: var(--vp-c-text-1);
  text-decoration: none;
  border-radius: 6px;
  transition: background 0.15s, color 0.15s;
}

.mobile-ext-item:hover {
  background: var(--vp-c-default-soft);
  color: var(--vp-c-brand);
}

.mobile-ext-item-icon {
  flex-shrink: 0;
  width: 22px;
  height: 22px;
  border-radius: 5px;
  object-fit: contain;
}

.mobile-ext-item-name {
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  line-height: 1.3;
}

/* External link icon */
.mobile-ext-icon {
  flex-shrink: 0;
  opacity: 0.55;
}

/* ── Responsive ──────────────────────────────────────── */

/* ≥768px: fix flex order — desktop-nav(1) | NavIconsMore(2) | hamburger(3)
   VPNavBarExtra is hidden via custom.css; VPNavBarAppearance at ≥1280px gets order:2 there */
@media (min-width: 768px) {
  .desktop-nav    { order: 1; }
  .nav-slot-more  { order: 2; }
}

/* Tablet (768px – 959px): tighter spacing to fit nav links */
@media (min-width: 768px) and (max-width: 959px) {
  .vp-nav-link {
    padding: 0 7px;
    font-size: 13px;
  }

  :deep(.ext-trigger) {
    padding: 0 7px;
    font-size: 13px;
  }
}

/* Mobile (< 768px): hide desktop nav, use hamburger drawer */
@media (max-width: 767px) {
  .desktop-nav { display: none; }
}

/* Very narrow screens: extensions list in a single column */
@media (max-width: 450px) {
  .mobile-menu-ext-grid {
    grid-template-columns: 1fr;
  }
}
</style>
