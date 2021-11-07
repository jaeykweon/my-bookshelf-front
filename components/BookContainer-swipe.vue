<template>
    <section class="lg:px-20 md:px-10 px-2 min-w-full flex justify-center ">
            <ul class="sm:w-144 min-w-full border-b-2 inline-flex flex-wrap justify-items-center justify-between">
                <div class="w-1/2 pl-2 border-l-2 block">
                    <li v-for="oddIdBook in paginatedBooks[0]" :key="oddIdBook.id" class="sm:w-64 w-36 py-3 block m-auto justify-center" >
                        <div>
                            <span class="bg-blue-600 text-gray-200 text-xs px-2 py-1 rounded-full">신규</span>
                        </div>
                        <nuxt-link :to="{path: '/detail', query:{ book_id:`${oddIdBook.id}`}}">
                            <img class="filter drop-shadow-xl pt-1" :src="oddIdBook.img_src" />
                        </nuxt-link>
                    </li>
                </div>
                <div class="w-1/2 pr-2 border-r-2">
                    <li v-for="evenIdBook in paginatedBooks[1]" :key="evenIdBook.id" class="sm:w-64 w-36 py-3 block m-auto justify-center" >
                        <div>
                            <span class="bg-blue-600 text-gray-200 text-xs px-2 py-1 rounded-full">신규</span>
                        </div>
                        <nuxt-link :to="{path: `/detail?book_id=${evenIdBook.id}`}">
                            <img class="filter drop-shadow-xl pt-1" :src="evenIdBook.img_src" />
                        </nuxt-link>
                    </li>
                </div>
            </ul>

            <!-- for swipe  -->
            <!-- <div class="sm:w-144 min-w-full inline-flex flex-wrap justify-items-center justify-between">
                <div class="swiper-wrapper">

                    <div v-for="(index,eachBookContainer) in paginatedBooks" :key="index" class="swiper-slide inline-flex border-l-2 border-r-2 border-b-2">
                    
                        <div class="w-1/2 pl-2 block">
                            <li v-for="oddIdBook in eachBookContainer[0]" :key="oddIdBook.id" class="sm:w-64 w-36 py-3 flex m-auto justify-center" >
                                <nuxt-link :to="{path: `/detail?book_id=${oddIdBook.id}`}">
                                        <img class="filter drop-shadow-xl" :src="oddIdBook.img_src" />
                                </nuxt-link>
                            </li>
                        </div>
                        <div class="w-1/2 pr-2 ">
                            <li v-for="evenIdBook in eachBookContainer[1]" :key="evenIdBook.id" class="sm:w-64 w-36 py-3 flex m-auto justify-center" >
                                <nuxt-link :to="{path: `/detail?book_id=${evenIdBook.id}`}">
                                    <img class="filter drop-shadow-xl" :src="evenIdBook.img_src" />
                                </nuxt-link>
                            </li>
                        </div>
                    </div>
                </div>
            </div> -->

            <!-- for swipe  -->
            <!-- <div class="sm:w-144 min-w-full inline-flex flex-wrap justify-items-center justify-between">
                <div class="swiper-wrapper">

                    <div class="swiper-slide inline-flex border-l-2 border-r-2 border-b-2">
                    
                        <div class="w-1/2 pl-2 block">
                            <li v-for="oddIdBook in paginatedBooks[0]" :key="oddIdBook.id" class="sm:w-64 w-36 py-3 flex m-auto justify-center" >
                                <nuxt-link :to="{path: `/detail?book_id=${oddIdBook.id}`}">
                                        <img class="filter drop-shadow-xl" :src="oddIdBook.img_src" />
                                </nuxt-link>
                            </li>
                        </div>
                        <div class="w-1/2 pr-2 ">
                            <li v-for="evenIdBook in paginatedBooks[1]" :key="evenIdBook.id" class="sm:w-64 w-36 py-3 flex m-auto justify-center" >
                                <nuxt-link :to="{path: `/detail?book_id=${evenIdBook.id}`}">
                                    <img class="filter drop-shadow-xl" :src="evenIdBook.img_src" />
                                </nuxt-link>
                            </li>
                        </div>
                    </div>
                </div>
            </div> -->


    </section>
</template>


<script>

import bookData from 'static/.test/books.json';

export default {
    name: 'App',
    data(){
        return {
            page : this.$route.query.page || 1,
            books : bookData
        }
    },
    head: {
        script: [
            {src: "https://unpkg.com/swiper/swiper-bundle.js"},
            {src: "https://unpkg.com/swiper/swiper-bundle.min.js"}
        ],
        link: [
            {
                rel: "stylesheet",
                href: "https://unpkg.com/swiper/swiper-bundle.css"
            },
            {
                rel: "stylesheet",
                href: "https://unpkg.com/swiper/swiper-bundle.min.css"
            }
        ]
    },
    computed: {
        paginatedBooks() {
            const paginatedBooks = [];
            let eachSwipeContainer = [[],[]];
            for (let i=0; i<this.books.length; i++){
                if(i%2 === 0){
                    eachSwipeContainer[0].push(this.books[i])
                }
                else {
                    eachSwipeContainer[1].push(this.books[i]);
                }
                if((i+1)%6===0 || i+1 === this.books.length){
                    paginatedBooks.push(eachSwipeContainer);
                    eachSwipeContainer = [[],[]];
                }
            }// endfor
            
            console.log("paginatedBooks", paginatedBooks[this.page - 1]);
            return paginatedBooks[this.page - 1]
        }
    }
}
</script>