<template>
    <section class="bg-gray-300 min-h-screen">
        <header>
            <Header />
        </header>
        <main class="mx-auto max-w-6xl min-h-screen px-3 md:px-0 mb-3 mt-3">
            <Messages />
            <Breadcrumb />
            <CookieBanner />
            <slot />
        </main>
        <footer class="">
            <Footer />
        </footer>
    </section>
</template>
<script setup lang="ts">
import './main.css';
import tracking from '~/util/tracking';
import { useBreadcrumbStore } from '~/stores/breadcrumb';
import Footer from '~/components/Footer.vue';
import Header from '~/components/Header.vue';

const store = useBreadcrumbStore();

onMounted(() => {
    tracking.trackPage()
    store.clear()
});
</script>