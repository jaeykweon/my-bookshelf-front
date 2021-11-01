<template>
    <section class="lg:px-20 md:px-10 px-2 min-w-full flex justify-center ">
        <!-- <div class="  px-5 flex-row  items-center text-center ">  -->
            <ul class="sm:w-144 inline-flex flex-wrap justify-center">
                <nuxt-link :to="{
					path: '/detail',
				}">
                    <li class="sm:w-64 w-40 text-center">
                        <img src="http://image.kyobobook.co.kr/images/book/xlarge/727/x9788960883727.jpg"/>
                    </li>
                </nuxt-link>
                <li class="sm:w-64 w-40 text-center">
                    책 내용 2
                </li>
                <li class="sm:w-64 w-40 text-center">
                    책 내용 3
                </li>
                <li class="sm:w-64 w-40 text-center">
                    책 내용 4
                </li>
            </ul>
        <!-- </div> -->
    </section>
</template>