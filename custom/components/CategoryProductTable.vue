<template>
    <div class="overflow-x-auto">
        <table class="table table-zebra">
            <!-- head -->
            <thead>
                <tr>
                    <th>#</th>
                    <th>Name</th>
                    <th>Price</th>
                    <th class="flex justify-end">
                        <span>Action</span>
                    </th>
                </tr>
            </thead>
            <tbody>
                <!-- row 1 -->
                <tr v-for="(product, index) in products" :key="product.id" :class="{
                    'bg-white': index % 2 == 0,
                    'bg-base-200': index % 2 == 1,
                }">
                    <th>{{ product.number }}</th>
                    <td>
                        <a :href="'/de/product/' + product.slug + '.html'">
                            {{ product.name }}
                        </a>
                    </td>
                    <th>{{ product.price.toFixed(2) }} €</th>
                    <td></td>
                    <td class="flex justify-end space-x-3">
                        <a :href="'/de/product/tshirt-bowling-1.html'" :class="{
                            'btn-neutral': index % 2 == 0,
                            'btn-secondary': index % 2 == 1,
                        }" class="btn btn-sm">
                            <Fa :icon="faCircleInfo" />
                        </a>
                        <button class="btn btn-sm" :class="{
                            'btn-neutral': index % 2 == 0,
                            'btn-secondary': index % 2 == 1,
                        }">
                            <Fa :icon="faShoppingCart" />
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script setup lang="ts">
import { faShoppingCart, faCircleInfo } from "@fortawesome/free-solid-svg-icons";
import PocketBase from "pocketbase";
import { storeToRefs } from "pinia";
import { usePocketbaseStore } from "~/stores/pocketbase";
import { onMounted, ref } from "vue";

const store = usePocketbaseStore();
const { url } = storeToRefs(store);
const pb = new PocketBase(url.value);
const products: Ref = ref([]);

onMounted(async () => {
    products.value = (await pb.collection('products').getList(1, 25, {
        filter: 'category="' + identifier + '"'
    })).items
});

const { identifier } = defineProps({
    identifier: {
        type: String,
        required: true,
    }
});
</script>
