<script setup>
import { Link } from "@inertiajs/vue3";

defineProps({
    meta: {
        type: Object,
        required: true
    }
})

const pageUrl = (url) => {
    const { pathname, search } = new URL(url, window.location.origin);
    // console.log(pathname, search);
    return `${pathname}${search}`;
}
</script>

<template>
    <nav class="flex items-center flex-column flex-wrap md:flex-row justify-between py-2 px-4" aria-label="Table navigation">
        <span class="text-sm font-normal text-gray-700 mb-4 md:mb-0 block w-full md:inline md:w-auto">Showing 
            <span class="font-semibold text-gray-700">{{ meta.from }}-{{ meta.to }}</span> of 
            <span class="font-semibold text-gray-700">{{ meta.total }}</span>
        </span>
        <ul class="inline-flex -space-x-px rtl:space-x-reverse text-sm h-8">
            <li v-for="(link, index) in meta.links" :key="index">
                <Link
                    v-if="link.url"
                    preserve-scroll
                    :href="pageUrl(link.url)"
                    class="flex items-center justify-center px-3 h-8 ms-0"
                    :class="{
                        'leading-tight text-gray-500 hover:text-gray-700': !link.active,
                        'text-blue-600 hover:text-blue-700': link.active,
                    }"
                    v-html="link.label"
                />
                <span
                    v-else
                    class="flex items-center justify-center px-3 h-8 ms-0 text-stone-400"
                    v-html="link.label"
                />
            </li>
        </ul>
    </nav>
</template>