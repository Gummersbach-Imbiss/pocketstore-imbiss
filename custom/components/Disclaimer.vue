<template>
    <div class="mx-3 xl:mx-auto">
        <section class="alert alert-warning flex justify-between">
            <Fa :icon="faCircleInfo" color="white" />
            <p class="text-sm text-white font-bold text-center block">
                Hallo Welt
            </p>
            <Fa :icon="faCircleInfo" color="white" />
        </section>
    </div>
</template>

<script lang="ts" setup>
import { faCircleInfo } from '@fortawesome/free-solid-svg-icons'
</script>