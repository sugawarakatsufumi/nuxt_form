<template>
  <div class="container">
    <h1>RESTお問い合わせフォーム {{userData.status}}</h1>
    <div class="confirm" :class="userData.confDispClass">
      <div class="form-group">
        <label>名前</label>
        <p>{{userData.name}}</p>
      </div>
      <div class="form-group">
        <label>メールアドレス</label>
        <p>{{userData.email}}</p>
      </div>
      <div class="form-group">
        <label>タイトル</label>
        <p>{{userData.title}}</p>
      </div>
      <div class="form-group">
        <label>本文</label>
        <p>{{userData.msg}}</p>
      </div>
      <div class="form-group">
        <label>csrf</label>
        <p>{{userData.csrf}}</p>
      </div>
      <button type="submit" class="btn btn-secondary" @click="backEntry">戻る</button>
      <button type="submit" class="btn btn-primary" @click="sendBackend">送信する</button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      userData: {
        // 初期値を入れる
        name: this.$route.query.name,
        email:this.$route.query.email,
        title:this.$route.query.title,
        msg:this.$route.query.msg,
        status:'確認',
        csrf:this.$route.query.csrf,
      }
    }
  },
  methods:{
    backEntry: function(e){
      this.$router.push({
        name:"index",
        query:{
          name:this.userData.name,
          email:this.userData.email,
          title:this.userData.title,
          msg:this.userData.msg
          }
      });
      event.preventDefault()
    },
    async sendBackend(e){
      // 取得先のURL
      const url = "http://localhost/mail_backend.php";
      // リクエスト
      const sendData = this.userData;
      delete sendData.status;
      const response = await this.$axios.$get(url,{
        params:sendData
      });
      //this.userData.status = '送信完了';
      console.log("この内容で送信:"+response);
      // 配列で返ってくるのでJSONにして返却
      //return {
      //    posts: response
      //};
      this.$router.push({name:'thanks'});
      event.preventDefault();
    },
  }
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
