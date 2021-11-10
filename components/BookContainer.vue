<template>
    <!-- <section class="lg:px-20 md:px-10 px-2 min-w-full flex justify-center ">
            <ul class="sm:w-144 min-w-full border-b-2 inline-flex flex-wrap justify-items-center justify-between">
                <div class="w-1/2 pl-2 border-l-2 block">
                    <li v-for="oddIdBook in paginatedBooks[0]" :key="oddIdBook.id" class="sm:w-64 w-36 py-3 block m-auto justify-center" >
                        <div class="">
                            https://web2tailwind.com/component/badge 
                            <span v-if="oddIdBook.state.new" class="inline-block bg-blue-600 text-gray-200 text-xs px-2 py-1 rounded-full">신규</span>
                            <span v-if="oddIdBook.state.on_air" class="inline-block bg-gray-600 text-gray-100 text-xs px-2 py-1 rounded-full">대출</span>
                            <span v-if="oddIdBook.state.finished" class="inline-block bg-green-400 text-gray-100 text-xs px-2 py-1 rounded-full">읽음</span>
                        </div>
                        <nuxt-link :to="{path: '/detail', query:{ book_id:`${oddIdBook.id}`}}">
                            <img class="w-36 h-52 filter drop-shadow-xl pt-1 " :src="oddIdBook.img_src" />
                        </nuxt-link>
                    </li>
                </div>
                <div class="w-1/2 pr-2 border-r-2">
                    <li v-for="evenIdBook in paginatedBooks[1]" :key="evenIdBook.id" class="sm:w-64 w-36 py-3 block m-auto justify-center" >
                        <div class="inline">
                            <div v-if="evenIdBook.state.new" class="inline-block bg-blue-600 text-gray-200 text-xs px-2 py-1 rounded-full">신규</div>
                            <div v-if="evenIdBook.state.on_air" class="inline-block bg-gray-600 text-gray-100 text-xs px-2 py-1 rounded-full">대출</div>
                            <div v-if="evenIdBook.state.finished" class="inline-block bg-green-400 text-gray-100 text-xs px-2 py-1 rounded-full">읽음</div>
                        </div>
                        <nuxt-link :to="{path: `/detail?book_id=${evenIdBook.id}`}">
                            <img class="w-36 h-52 filter drop-shadow-xl pt-1" :src="evenIdBook.img_src" />
                        </nuxt-link>
                    </li>
                </div>
            </ul>
    </section> -->

    <section class="lg:px-20 md:px-10 px-2 min-w-full flex justify-center ">
            <ul class="sm:w-144 min-w-full border-b-2 inline-flex flex-wrap justify-items-center justify-center">
                <div class="w-full px-2 border-l-2 border-r-2 m-auto inline justify-around">
                    <li v-for="book in sortedBooks" :key="book.id" class="sm:w-64 w-36 py-3 mx-2 inline-block justify-center" >
                        <div class="text-left">
                            <!-- https://web2tailwind.com/component/badge -->
                            <span v-if="book.state.new" class="inline-block bg-blue-600 text-gray-200 text-xs px-2 py-1 rounded-full">신규</span>
                            <span v-if="book.state.on_air" class="inline-block bg-gray-600 text-gray-100 text-xs px-2 py-1 rounded-full">대출</span>
                            <span v-if="book.state.finished" class="inline-block bg-green-400 text-gray-100 text-xs px-2 py-1 rounded-full">읽음</span>
                        </div>
                        <div class="w-36 h-52">
                            <nuxt-link :to="{path: '/detail', query:{ book_id:`${book.id}`}}">
                                <img class="transform transition motion-reduce:transform-none hover:scale-110 rounded-md duration-50 pt-1 filter drop-shadow-xl" :src="book.img_src" />
                            </nuxt-link>
                        </div>
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
            page : this.$route.query.page || 1,
            books : bookData,
            categoryList : typeof this.$route.query.category === "string"? this.$route.query.category.split(','): this.$route.query.category,
            stateList : typeof this.$route.query.state === "string"? this.$route.query.state.split(',') : this.$route.query.state
        }
    },
    computed: {

        sortedBooks(){
            const sortedBooks = [];
            for (const eachBook of this.books){
                console.log("this.categoryList", this.categoryList);
                
                if(this.categoryList && !this.categoryList?.includes(eachBook.category.main)) {  // this.categoryList && 
                    // 카테고리 조건으로 검색했고 그 검색어에 없는 경우
                    continue
                };

                let stateCheck = false;
                if(this.stateList){
                    console.log("this.stateList", this.stateList);
                    for(const _state of this.stateList){ 
                        console.log("_state", _state);
                        if(eachBook.state[_state]){
                            console.log("eachBook.state[_state]", eachBook.state[_state]);
                            stateCheck = true;
                            break
                        }
                    }
                }
                else{stateCheck = true}
                
                if(stateCheck){
                    sortedBooks.push(eachBook);
                }
            }
            return sortedBooks
        }
    }
}
</script>