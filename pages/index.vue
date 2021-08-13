<template>
    <div>
    <ul>
      <li><nuxt-link :to="{name:'index'}">HOME</nuxt-link></li>
      <li><nuxt-link :to="{name:'abouts'}">ABOUT</nuxt-link></li>
      <li><nuxt-link :to="{name:'news',params:{newsId:10010}}">NEWS</nuxt-link></li>
    </ul>
  </div>
</template>

<script>
export default {};
</script>
