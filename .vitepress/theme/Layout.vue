<script lang="ts" setup>
import DefaultTheme from 'vitepress/theme'
import { useData } from 'vitepress'
import ShortcutsList from './components/ShortcutsList.vue'
import ImplVariants from './components/implvariants/ImplVariants.vue'
import NavScreenMenuItem from './components/implvariants/NavScreenMenuItem.vue'
import NotFound from './components/NotFound.vue'
import Ribbon from './components/Ribbon.vue'
// import ScrollToTop from './components/ScrollToTop.vue'

const isPreview = !!import.meta.env.VITE_CAPIRE_PREVIEW

const { Layout } = DefaultTheme
const { frontmatter } = useData()

</script>

<template>

  <Layout>
    <template #layout-top>
      <ScrollToTop />
      <slot name="layout-top" />
    </template>
    <template #doc-top>
      <slot name="doc-top" />
    </template>
    <template #not-found>
      <NotFound />
    </template>
    <template #nav-bar-title-after>
      <slot name="nav-bar-title-after" />
      <div class="ImplVariantsInNavbar" v-if="frontmatter?.layout !== 'home'">
        <ImplVariants/>
      </div>
    </template>
    <template #nav-bar-content-before>
      <slot name="nav-bar-content-before" />
    </template>
    <template #nav-bar-content-after>
      <slot name="nav-bar-content-after" />
    </template>
    <template #nav-screen-content-after>
      <NavScreenMenuItem/>
      <slot name="nav-screen-content-after" />
    </template>
  </Layout>

  <Ribbon v-if="isPreview">
    DEV PREVIEW<br>
    See <a href="https://cap.cloud.sap" target="_blank" rel="noopener noreferrer">cap.cloud.sap</a>
  </Ribbon>

  <ShortcutsList />

</template>

<style scoped>

.ImplVariantsInNavbar {
  margin-left: auto;
}

@media (max-width: 960px) {
  .ImplVariantsInNavbar {
    display: none;
  }
}
</style>