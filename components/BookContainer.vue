<template>
    <section class="lg:px-20 md:px-10 px-2 min-w-full justify-center">
            <div class="min-w-full">
                    <ul class="grid grid-cols-2 w-1/2">
                        <li v-for="bookCategory in bookCategories" :key="bookCategory" class="flex flex-wrap items-center">
                            <input 
                                v-model="selectedCategoryList" 
                                :value="bookCategory" 
                                class="text-indigo-500 w-5 h-5 mr-2 focus:ring-indigo-400 focus:ring-opacity-25 border border-gray-300 rounded" 
                                type="checkbox" 
                                @change="addCategoryToParam()"
                            />
                            <label>{{ bookCategory }}</label>
                        </li>
                    </ul>
            </div>

            <ul class="w-full px-2 border-2 m-auto grid justify-items-center 2xl:grid-cols-7 xl:grid-cols-6 lg:grid-cols-5 md:grid-cols-4 sm:grid-cols-3 grid-cols-2">
                <li v-for="book in sortedBooks" :key="book.id" class="sm:w-44 w-36 py-3 mx-2 inline-grid text-center justify-center" >
                    <div class="text-left inline-block">
                        <!-- https://web2tailwind.com/component/badge -->
                        <span v-if="book.state.new" class="inline-block bg-blue-600 text-gray-200 text-xs px-2 py-1 rounded-full">신규</span>
                        <span v-if="book.state.on_air" class="inline-block bg-gray-600 text-gray-100 text-xs px-2 py-1 rounded-full">대출</span>
                        <span v-if="book.state.finished" class="inline-block bg-green-400 text-gray-100 text-xs px-2 py-1 rounded-full">읽음</span>
                    </div>
                    <div class="w-36 h-52 flex flex-wrap content-center">
                        <nuxt-link :to="{path: '/detail', query:{ book_id:`${book.id}`}}">
                                <img class="transform transition motion-reduce:transform-none hover:scale-110 rounded-md duration-50 max-h-52 pt-1 filter drop-shadow-xl" :src="book.img_src" />
                        </nuxt-link>
                    </div>
                </li>
            </ul>
    </section>
</template>


<script>

import bookData from 'static/.test/books.json';
import bookCategories from 'static/.test/bookCategories.json';

export default {
    name: 'App',
    data(){
        const selectedCategoryList = [];
        if (typeof this.$route.query.category === "string"){
            for (const each of this.$route.query.category.split(',')){
                selectedCategoryList.push(each);
            }
        }else if(this.$route.query.category){
            for (const each of this.$route.query.category){
                selectedCategoryList.push(each);
            }
        }
        return {
            page : this.$route.query.page || 1,
            books : bookData,
            bookCategories,
            selectedCategoryList,
            stateList : typeof this.$route.query.state === "string"? this.$route.query.state.split(',') : this.$route.query.state
        }
    },
    computed: {
        sortedBooks(){
            const sortedBooks = [];
            console.log("this.selectedCategoryList", this.selectedCategoryList);
            for (const eachBook of this.books){
                
                if(this.selectedCategoryList?.length > 0 && !this.selectedCategoryList?.includes(eachBook.category.main)) {  // this.categoryList && 
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
                else{
                    stateCheck = true
                }

                if(stateCheck){
                    sortedBooks.push(eachBook);
                }
            }
            return sortedBooks
        },
    },
    watch:{
        // '$route.query'(){
        //     this.sortedBooks()
        // }
    },
    methods:{
        addCategoryToParam(){
            console.log("this.selectedCategoryList", this.selectedCategoryList);
            this.$router.push({query:{state: this.selectedCategoryList}})
        }
    }
}
</script>