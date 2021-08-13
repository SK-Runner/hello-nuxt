<template>
    <div>
        <h2>新闻</h2>
        <p>新闻ID：{{$route.params.newsId}}</p>
        <ul>
            <li>
                <nuxt-link :to="{name:'index'}">HOME</nuxt-link>
                <nuxt-link :to="{name:'news-id',params:{id:'新闻内容'}}">进入News-1</nuxt-link>
                <nuxt-link :to="{name:'news-id',params:{id:'新闻内容2'}}">进入News-2</nuxt-link>
            </li>
        </ul>
    </div>
</template>