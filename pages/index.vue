<template>
  <div class="container">
    <h1>RESTお問い合わせフォーム {{userData.status}}</h1>
    <form class="entry" @submit.prevent="confirm" method="post">
      <div class="form-group">
        <label>名前</label>
        <input class="form-control" type="text" name="name" v-model="userData.name" />
      </div>
      <div class="form-group">
        <label>メールアドレス*</label>
        <input type="text" class="form-control" name="email" v-model="userData.email" />
        <small>{{emailCheck}}</small>
      </div>
      <div class="form-group">
        <label>タイトル</label>
        <input class="form-control" type="text" name="title" v-model="userData.title" />
      </div>
      <div class="form-group">
        <label>本文</label>
        <textarea class="form-control" name="msg" v-model="userData.msg"></textarea>
      </div>
      <input type="hidden" name="csrf" v-model="posts.csrf">
      <button type="submit" class="btn btn-primary">確認画面</button>
    </form>
  </div>
</template>

<script>
export default {
  async asyncData(context) {
    // 取得先のURL
    const url = "http://localhost/mail_backend.php";
    // リクエスト（Get）
    const response = await context.$axios.$get(url);
    console.log(response);
    // 配列で返ってくるのでJSONにして返却
    return {
        posts: response
    };
  },
  data () {
    return {
      userData: {
        // 初期値を入れる
        name: this.$route.query.name? this.$route.query.name: "",
        email:this.$route.query.email? this.$route.query.email: '',
        title:this.$route.query.title? this.$route.query.title: '',
        msg:this.$route.query.msg? this.$route.query.msg: '',
        status:'入力',
        csrf:'',
      },
      emailCheck:'',
    }
  },
  methods:{
    async confirm(e){
      //alert('test');
      if(this.userData.email != ''){
        this.$router.push({
          name:"conf",
          query:{
            name:this.userData.name,
            email:this.userData.email,
            title:this.userData.title,
            msg:this.userData.msg,
            csrf:this.posts.csrf,
          }
        });
      }else{
        this.emailCheck = 'アドレスが未入力です'
      }
      event.preventDefault()
    },
  },
  watch:{
    "userData.email": function(new_value, old_value){
      if(this.userData.email !=''){
        this.emailCheck = '';
      }
    },
  }
}
</script>

<style>

</style>
