<template>
    <section class="lg:px-20 md:px-10 min-w-full flex justify-center ">
            <ul class="sm:w-144 min-w-full px-2 inline-flex flex-wrap justify-items-center justify-between">
                <div class="w-1/2 pl-2 border-l-2 block">
                    <li v-for="oddIdBook in sortedBooks[0]" :key="oddIdBook.id" class="sm:w-64 w-36 py-3 flex m-auto justify-center" >
                        <nuxt-link :to="{path: `/detail?book_id=${oddIdBook.id}`}">
                                <img :src="oddIdBook.img_src" />
                        </nuxt-link>
                    </li>
                </div>
                <div class="w-1/2 pr-2 border-r-2">
                    <li v-for="evenIdBook in sortedBooks[1]" :key="evenIdBook.id" class="sm:w-64 w-36 py-3 flex m-auto justify-center" >
                        <nuxt-link :to="{path: `/detail?book_id=${evenIdBook.id}`}">
                            <img :src="evenIdBook.img_src" />
                        </nuxt-link>
                    </li>
                </div>
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
    },
    computed: {
        sortedBooks() {
            const sortedBooks = [[],[]];
            for (let i=0; i<this.books.length; i++){
                if(i%2 === 0) {sortedBooks[0].push(this.books[i])}
                else {sortedBooks[1].push(this.books[i])}
            }
            return sortedBooks
        }
    }
}
</script>
