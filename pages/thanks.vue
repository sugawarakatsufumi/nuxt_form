<template>
  <div class="container">
    <h1>RESTお問い合わせフォーム {{userData.status}}</h1>
    <div class="thank">
      <p>送信完了しました</p>
      <nuxt-link to="/" class="btn btn-primary">戻る</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      userData: {
        // 初期値を入れる
        name: '',
        email:'',
        title:'',
        msg:'',
        status:'送信完了',
      }
    }
  },
}
</script>

<style>
.container {
}
.disp-block{
  display:block;
}
.disp-none{
  display:none;
}

</style>
