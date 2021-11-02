<template>
    <section class="lg:px-20 md:px-10 px-5z min-w-full flex justify-center ">

            <ul class="sm:w-144 inline-flex flex-wrap justify-items-center justify-between">
                
                <li v-for="book in books" :key="book.id" class="sm:w-64 w-40 px-2 py-2 text-center" >
                    <nuxt-link :to="{path: '/detail'}">
                        <img :src="book.img_src" />
                    </nuxt-link>
                </li>
                
            </ul>

    </section>
</template>


<script>

import bookData from 'static/.test/books.json';

export default {
    name: 'App',
    data(){
        return {
            books : bookData
        }
    }
}
</script>
