<script setup lang="ts">
import { onMounted, onBeforeUnmount, computed } from 'vue'
import DefaultTheme from 'vitepress/theme'
import { useRoute } from 'vitepress'
import GoogleTranslate from './components/GoogleTranslate.vue'
import AutoImageZoom from './components/AutoImageZoom.vue'
import PromoBar from './components/PromoBar.vue'
import ExtensionsMegaMenu from './components/ExtensionsMegaMenu.vue'
import VPSwitchAppearance from 'vitepress/dist/client/theme-default/components/VPSwitchAppearance.vue'

const { Layout } = DefaultTheme
const route = useRoute()
const isHome = computed(() => route.path === '/')

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

    <!-- Mobile overlay: flat extensions list + external nav links -->
    <template #nav-screen-content-before>
      <div class="mobile-ext-section">
        <p class="mobile-ext-heading">Extensions</p>
        <nav class="mobile-ext-links">
          <a href="/akeneo-migration/">Akeneo Migration</a>
          <a href="/ai-product-feed-openai/">AI Product Feed</a>
          <a href="/auto-sku-generator/">Auto SKU Generator</a>
          <a href="/aws-integration/">AWS Integration</a>
          <a href="/bagisto/">Bagisto</a>
          <a href="/bigcommerce/">BigCommerce</a>
          <a href="/azure-integration/">Azure Integration</a>
          <a href="/cloudflare-r2-integration/">Cloudflare R2</a>
          <a href="/cs-cart/">CS-Cart</a>
          <a href="/dam/">DAM</a>
          <a href="/deepl/">DeepL Translator</a>
          <a href="/erpnext/">ERPNext</a>
          <a href="/google-shopping/">Google Shopping</a>
          <a href="/job-scheduler/">Job Scheduler</a>
          <a href="/maker-checker-workflow/">Maker Checker</a>
          <a href="/magento2/">Magento 2</a>
          <a href="/odoo-erp/">Odoo ERP</a>
          <a href="/pdf-generator/">PDF Generator</a>
          <a href="/prestashop/">PrestaShop</a>
          <a href="/public-image-url/">Public Image URL</a>
          <a href="/shopify/">Shopify</a>
          <a href="/supplier-data-portal/">Supplier Portal</a>
          <a href="/woocommerce/">WooCommerce</a>
          <a href="/woocommerce-wpml/">WooCommerce WPML</a>
        </nav>
        <div class="mobile-nav-links">
          <a href="https://docs.unopim.com/" target="_blank" rel="noopener noreferrer">User Guide</a>
          <a href="https://devdocs.unopim.com/" target="_blank" rel="noopener noreferrer">Dev Doc</a>
          <a href="https://unopim.com/en/contacts/" target="_blank" rel="noopener noreferrer">Contact Us</a>
        </div>
      </div>
    </template>

    <!-- Desktop: all nav links right of the search bar -->
    <template #nav-bar-content-after>
      <a href="/" class="vp-nav-link" :class="{ active: isHome }">Home</a>
      <ExtensionsMegaMenu />
      <a href="https://docs.unopim.com/" class="vp-nav-link" target="_blank" rel="noopener noreferrer">User Guide</a>
      <a href="https://devdocs.unopim.com/" class="vp-nav-link" target="_blank" rel="noopener noreferrer">Dev Doc</a>
      <a href="https://unopim.com/en/contacts/" class="vp-nav-link" target="_blank" rel="noopener noreferrer">Contact Us</a>
      <div class="vp-nav-icons">
        <VPSwitchAppearance class="vp-nav-appearance" />
        <a
          class="vp-nav-icon vp-nav-icon--github"
          href="https://github.com/unopim"
          target="_blank"
          rel="noopener noreferrer"
          aria-label="UnoPim on GitHub"
          title="GitHub"
        >
          <svg viewBox="0 0 24 24" width="20" height="20" aria-hidden="true">
            <path fill="currentColor" d="M12 .5C5.73.5.5 5.73.5 12c0 5.08 3.29 9.39 7.86 10.91.58.11.79-.25.79-.56 0-.28-.01-1.02-.02-2-3.19.69-3.87-1.54-3.87-1.54-.52-1.32-1.28-1.68-1.28-1.68-1.05-.72.08-.71.08-.71 1.16.08 1.77 1.19 1.77 1.19 1.03 1.77 2.7 1.26 3.36.96.1-.75.4-1.26.73-1.55-2.55-.29-5.23-1.28-5.23-5.7 0-1.26.45-2.28 1.19-3.08-.12-.29-.52-1.47.11-3.06 0 0 .97-.31 3.18 1.18a11.04 11.04 0 0 1 5.79 0c2.2-1.49 3.17-1.18 3.17-1.18.63 1.59.23 2.77.11 3.06.74.8 1.19 1.82 1.19 3.08 0 4.43-2.69 5.41-5.25 5.69.41.35.78 1.05.78 2.12 0 1.53-.01 2.76-.01 3.13 0 .31.21.68.8.56C20.22 21.38 23.5 17.08 23.5 12 23.5 5.73 18.27.5 12 .5Z"/>
          </svg>
        </a>
        <GoogleTranslate class="vp-nav-icon vp-nav-icon--translate" />
      </div>
    </template>
    <template #layout-bottom>
      <AutoImageZoom />
    </template>
  </Layout>
</template>

<style scoped>
/* ── Nav links (Home, User Guide, Dev Doc, Contact Us) ── */
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

/* ── Mobile extensions section ─────────────────────── */
.mobile-ext-section {
  padding: 12px 24px 4px;
  border-bottom: 1px solid var(--vp-c-divider);
  margin-bottom: 8px;
}

.mobile-ext-heading {
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--vp-c-text-3);
  margin: 0 0 8px;
}

.mobile-ext-links {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2px;
}

.mobile-ext-links a {
  display: block;
  padding: 7px 8px;
  font-size: 14px;
  font-weight: 500;
  color: var(--vp-c-text-1);
  text-decoration: none;
  border-radius: 6px;
  transition: background 0.15s, color 0.15s;
}

.mobile-ext-links a:hover {
  background: var(--vp-c-default-soft);
  color: var(--vp-c-brand);
}

/* ── Mobile external nav links ─────────────────────── */
.mobile-nav-links {
  display: flex;
  flex-direction: column;
  gap: 2px;
  padding: 8px 0 4px;
}

.mobile-nav-links a {
  display: block;
  padding: 7px 8px;
  font-size: 14px;
  font-weight: 500;
  color: var(--vp-c-text-1);
  text-decoration: none;
  border-radius: 6px;
  transition: background 0.15s, color 0.15s;
}

.mobile-nav-links a:hover {
  background: var(--vp-c-default-soft);
  color: var(--vp-c-brand);
}

/* Hide VitePress built-in appearance toggle (we render it manually) */
:deep(.VPNavBarAppearance) {
  display: none !important;
}

/* ── Nav icons ─────────────────────────────────────── */
.vp-nav-icons {
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
  padding-left: 0.75rem;
}

.vp-nav-icon {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 2rem;
  height: 2rem;
  padding: 0.25rem;
  border-radius: 9999px;
  color: var(--vp-c-text-1);
  transition: background-color 0.2s ease, color 0.2s ease;
}

.vp-nav-icon::before {
  content: '';
  position: absolute;
  left: -0.5rem;
  top: 50%;
  transform: translateY(-50%);
  width: 1px;
  height: 1.25rem;
  background-color: var(--vp-c-divider);
  pointer-events: none;
}

.vp-nav-icon:hover {
  background-color: var(--vp-c-default-soft);
  color: var(--vp-c-brand);
}

.vp-nav-icon :deep(img),
.vp-nav-icon :deep(svg) {
  display: block;
}

.vp-nav-appearance {
  display: inline-flex;
  align-items: center;
}
</style>
