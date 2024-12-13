<template>
    <section class="page">
        <div class="max-w-6xl grid grid-cols-6 gap-3 px-3 py-3 bg-white rounded-lg mx-3 xl:mx-auto">
            <div class="col-span-6">
                <div class="bg-cover h-64 bg-cover rounded-lg flex justify-end items-end"
                    style="background-image:url('/luca-bravo-8x_fFNrmeDk-unsplash.jpg')">
                    <span class="text-white font-bold text-lg mr-3 mb-3">
                        Imbiss Jonny, Kölnerstrasse 123, 51702 Bergneustadt
                    </span>
                </div>
            </div>
            <div v-for="item in items" :key="item.id" class="col-span-6 md:col-span-3">
                <a href="/de/category/food" class="btn btn-primary btn-block">{{ item.name }}</a>
                <CategoryProductTable :identifier="item.id" />
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
import PocketBase from 'pocketbase';
import { storeToRefs } from 'pinia';
import { usePocketbaseStore } from '~/stores/pocketbase';
import { useBreadcrumbStore } from '~/stores/breadcrumb';
import { onMounted } from 'vue';
import CategoryProductTable from '../components/CategoryProductTable.vue';

const store = usePocketbaseStore();
const { url } = storeToRefs(store);
const pb = new PocketBase(url.value);

const storeBreadcrumb = useBreadcrumbStore();
storeBreadcrumb.clear();

const items = ref([]);

onMounted(() => {
    load();
});

const load = async function () {
    items.value = (await pb.collection('categories').getList(1, 10)).items;
}
</script>