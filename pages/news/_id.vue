<template>
    <div>
        <h2>News-Content</h2>
        <p>{{$route.params.id}}</p>
        <ul>
            <li>
                <a href="/">HOME</a>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    validate({params}){
        // 判断动态路由内容是否以数字结尾
        return /\d$/.test(params.id)
    }
}
</script>

<style>

</style>