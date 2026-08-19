<script setup lang="ts">
import { onMounted, onBeforeUnmount, computed, ref } from 'vue'
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
const mobileExtOpen = ref(false)

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
  padding: 0 24px;
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
  grid-template-columns: 1fr 1fr;
  gap: 2px;
  padding-bottom: 12px;
}

.mobile-menu-ext-grid a {
  display: block;
  padding: 7px 8px;
  font-size: 13.5px;
  font-weight: 500;
  color: var(--vp-c-text-1);
  text-decoration: none;
  border-radius: 6px;
  transition: background 0.15s, color 0.15s;
}

.mobile-menu-ext-grid a:hover {
  background: var(--vp-c-default-soft);
  color: var(--vp-c-brand);
}

/* External link icon */
.mobile-ext-icon {
  flex-shrink: 0;
  opacity: 0.55;
}

/* Hide VitePress built-in nav bar appearance toggle (we render our own on desktop) */
:deep(.VPNavBarAppearance) {
  display: none !important;
}

/* ── Nav icons ───────────────────────────────────────── */
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

/* ── Responsive ──────────────────────────────────────── */
@media (max-width: 959px) {
  /* Hide desktop-only nav block */
  .desktop-nav {
    display: none;
  }

  /* Hide our custom appearance toggle — mobile drawer has VitePress's built-in one */
  .vp-nav-appearance {
    display: none;
  }

  /* Compact icon row on tablet/mobile */
  .vp-nav-icons {
    gap: 0.25rem;
    padding-left: 0.25rem;
  }

  .vp-nav-icon {
    width: 1.75rem;
    height: 1.75rem;
  }
}

@media (max-width: 480px) {
  /* Remove divider line before icon group on very small screens */
  .vp-nav-icon::before {
    display: none;
  }
}
</style>
