<template>
  <div>
    <!-- header 1-->
    <div class="login-bg">
      <div class="login-title d-flex align-items-center">
        <!-- <img src="./img/bg_signin01.png" class="w-100" alt=""> -->
          <div class="col-2 ic-back"><img src="./img/ic_back.png" alt=""></div>
          <div class="col-8 text-center member-login">會員登入</div>
          <div class="col-2"></div>
      </div>
      <!-- logo & line -->
      <div class="position-relative">
        <div class="line"></div>
        <img src="./img/logo01.png" class="logo" alt="">
      </div>
    <!-- /header 1-->

    <!-- header 2 -->
      <!-- facevook/apple/google -->
      <div class="sign-box mt-5">
        <img src="./img/bt_facebook.png" class="bt-size">
        <img src="./img/bt_apple.png" class="bt-size">
        <img src="./img/bt_google.png" class="bt-size">
      </div>

      <!-- or -->
      <div class="mt-4">
        <div class="line-or">或</div>
      </div>
    
      <!-- input -->
      <form class="form-wrap">
        <div class="form-group">
          <label for="username" class="login-input-text">帳號 | 手機 | 電子信箱</label>
          <div class="input-username">
            <input type="text" name="username" v-model="username" list="usernamedata" class="form-control login-placeholder" v-bind:class="{ 'is-invalid': usernameError }" id="inputLogin" placeholder="5-50個英數字">
            <div v-if="emaildata.show" class="email-select">
              <ul class="email-select-list">
                <li v-for="(item) in emaildata.list" @click="emailSelect(item)">{{ item }}</li>
              </ul>
            </div>
            <div class="invalid-feedback">
              <img src="./img/ic_alerts-alt.png" class="img-pwd-err">{{ userErrMsg }}
            </div>

            <!-- <div>
              <EmailDropdown
                v-model="email"
                :defaultDomains="defaultDomains"
                :domains="domains"
                :maxSuggestions="5"
                placeholder=""
              />
            </div> -->

            <img src="./img/feather-ic-delete.png" v-if="this.username.length > 0" class="usernameClear" @click="usernameClear()">
          </div>
        </div>

        <div class="form-group">
          <label for="inputLoginPassword" class="login-input-text">密碼</label>
          <div class="input-pwd">
            <input type="password" v-model="password" v-bind:class="{ 'is-invalid': passwordError }" class="form-control login-placeholder" id="inputLoginPassword"  maxlength='20' placeholder="7-20個英數字">
            <div class="icon-eyes" @click="iconEye()"></div>
            <div class="invalid-feedback">
              <img src="./img/ic_alerts-alt.png" class="img-pwd-err">{{ passErrMsg }}
            </div>
          </div>
          
        </div>
       <!-- 記住帳號/忘記密碼 -->
        <div class="form-check">
          <input type="checkbox" class="form-check-input" id="check" />
          <label class="form-check-label" for="check">記住帳號</label>
          <a href="#" class="forgot">忘記密碼</a>
        </div>
        <!-- submit/enter btn -->
        <div class="btn-warp  d-flex justify-content-between">
          <div class="l-btn signup-btn" @click="signin()">註冊</div>
           <!--disable-->
          <div
            :class="['l-btn submit-btn',{'submit-active-btn':loginInfo }]"
            @click="loginSubmit()"
            data-toggle="modal"
            data-target="#myModal"
          >
            確定
          </div>
        </div>
      </form>
      <!-- Modal -->
      <HelloWorld/>
      <!-- <div
        class="modal fade"
        id="myModal"
        tabindex="-1"
        role="dialog"
        aria-labelledby="myModalTitle"
        aria-hidden="true"
      >
        <div class="modal-dialog modal-dialog-centered" role="document">
          <div class="modal-content">
            <div class="modal-header d-flex justify-content-center">
              <div class="modal-title-bg">
                <div class="modal-title text-center" id="myModalTitle">
                  提示
                </div>
              </div>

              <div
                type="button"
                class="modal-close"
                data-dismiss="modal"
                aria-label="Close"
              >
                <span aria-hidden="true">&times;</span>
              </div>
            </div>
            <div class="modal-body text-center">
              帳號或密碼輸入錯誤
            </div>
            <div class="modal-footer d-flex justify-content-center">
              <div class="l-btn submit-active-btn" data-dismiss="modal">確定</div>
            </div>
          </div>
        </div>
      </div> -->
    </div>
  </div>
</template>

<script>
  import $ from 'jquery'
  import HelloWorld from "../components/HelloWorld.vue";
  // import EmailDropdown from "../components/vue-email-dropdown.vue";
  // import "vue-email-dropdown/dist/vue-email-dropdown.css";

  export default {
    components: {
      HelloWorld,
      // EmailDropdown
    },

  data() {
    return {
        emaildata:{
          show:false,
          list:["gmail.com",
              "hotmail.com",
              "outlook.com",
              "yahoo.com"]
        },
        username: '',
        usernameError: false,
        userErrMsg: '',
        password: '',
        passwordError: false,
        passErrMsg: '',
        email: '',
        emailError: false,
        emailErrMsg: '',
        submitError: false,
        submitErrMsg: '',
        isModalVisible: false,
        checked: true,
      //   email: "",
      // domains: [
      //   "yourcompany.com",
      //   "gmx.de",
      //   "googlemail.com",
      //   "hotmail.fr",
      //   "hotmail.it",
      //   "web.de",
      //   "gmail.com",
      //   "yahoo.co.in",
      //   "yahoo.com",
      //   "yahoo.in"
      // ],
      // defaultDomains: [
      //   "gmail.com",
      //   "hotmail.com",
      //   "msn.com",
      //   "outlook.com",
      //   "yahoo.com"
      // ]
      }
    },

    watch: {
      username: function () {
      console.log("xxxx",this.username.indexOf('@'))
      this.firstUser = false
        if(this.vaildMobile() === true ) {
          console.log("aa")
          this.usernameError = false;
            this.userErrMsg = '';
            return
        } 
        if(this.vaildAcc() === true) {
          console.log("bb")
          this.usernameError = false;
            this.userErrMsg = '';
            return
        } 
        if(this.vaildEmail() === true) {
          console.log("cc")
          this.usernameError = false;
            this.userErrMsg = '';
            return
        } else {
          if(this.username.indexOf('@') > -1) {
            this.emaildata.show = true
            this.emailDomain()
            // this.emaildata.show = true
            // this.emaildata.list = [
            //   "gmail.com",
            //   "hotmail.com",
            //   "outlook.com",
            //   "yahoo.com"
            // ]
          }
        }
      },

      password: function () {
          var isText = /^[0-9A-Za-z]{7,20}$/ //密碼限7~20個英數字(不可空格)
          var include = /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{7,20}$/; //至少包括一個大小寫字母或數字
          var isFormat = /([[0-9A-Za-z])(\1){2,}|(abc|bcd|cde|def|efg|fgh|ghi|hij|ijk|jkl|klm|lmn|mno|nop|opq|pqr|qrs|rst|stu|tuv|uvw|vwx|wxy|xyz|ABC|BCD|CDE|DEF|EFG|FGH|GHI|HIJ|IJK|JKL|KLM|LMN|MNO|NOP|OPQ|PQR|QRS|RST|STU|TUV|UVW|VWX|WXY|XYZ|012|123|234|345|456|567|678|789)+/ //不可為連續英文、連號數字及3碼相同字重複(ex：123、456、ABC、dEF、111、aaa)
        
          if (this.password.length == 0) {
            this.passwordError = true;
            this.passErrMsg = '請輸入密碼';
          }
          else if (!isText.test(this.password)) {
            this.passwordError = true;
            this.passErrMsg = '密碼限7~20個英數字(不可空格)';
          }
        
          else if (isFormat.test(this.password)) {
              this.passwordError = true;
              this.passErrMsg = '不可為連續英文、連號數字及3碼相同字重複';
          }
        
          else if (!include.test(this.password)) {
              this.passwordError = true;
              this.passErrMsg = '至少包括一個大小寫字母或數字';
          }
        
          else {
              this.passwordError = false;
          }
      },
    },
    computed: {
      //相依的資料改變時才做計算方法
      loginInfo(){
        //判斷帳密是否成立 true+class
        if(this.username === '' && this.password === ''){
          return false
        }else if(this.username !== '' && this.password !== '' && this.passwordError === false)
          return true
      }
    },
    methods: {
      vaildAcc(){
        var isText = /^[A-Za-z0-9]{5,50}$/ 
        // console.log(isText.test(this.username))
        if (!isText.test(this.username)) {
            this.usernameError = true;
            this.userErrMsg = '輸入格式有誤';
            console.log('text',this.username)
            return false
          }
        return true 
      },
      vaildMobile(){
        var isMobile = /^09\d{8}$/
        // console.log(isMobile.test(this.username))
        if (!isMobile.test(this.username)) {
            this.usernameError = true;
            this.userErrMsg = '輸入格式有誤';
            console.log('isMobile',this.username)
            return false
          }
        return true 
      },
      vaildEmail(){
        var isEmail = /^\w+((-\w+)|(\.\w+))*\@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z]+$/
        // console.log(isEmail.test(this.username))
        if (!isEmail.test(this.username)) {
            this.usernameError = true;
            this.userErrMsg = '輸入格式有誤';
            this.emaildata.show = false 
            this.emaildata.list = []
            console.log('isEmail',this.username)
            return false
          }
        return true
      },
      // emailDomain(){
      //   this.emaildata.list.filter(function (element, index, self) {
      //       console.log('element',element)
      //     });
      // },
      emailDomain(){
        // let emailAll = this.emaildata.list[]
          let emaildata = ["gmail.com","hotmail.com","outlook.com","yahoo.com"];
          console.log(emaildata)
          let self = this
          console.log(this.username)

          if (this.username.split('@')[1]=== "" ){
            this.emaildata.list = emaildata
            return
          }

          this.emaildata.list = []

          let filter = emaildata.filter(function(item){
            console.log('self:',self.username.split('@')[1][0])
            console.log(item[0])
            if(item[0].indexOf(self.username.split('@')[1][0]) > -1 
            && self.username.split('@')[1]!== " " 
            ){
              console.log('indexOf',item)
              return item
            }
          })

          this.emaildata.list = filter
        },
      emailSelect(item) {
        console.log('key')
        this.username = this.username.split('@')[0] + '@'+ item
        this.emaildata.show = false
      },
      // 初始
      usernameClear(){
        this.username = ''
      },
      // 密碼顯示隱藏
      iconEye(){
        var x = document.getElementById("inputLoginPassword");
        if (x.type === "password") {
          x.type = "text";
          $(".icon-eyes").addClass("toggle-password");
        } else {
          x.type = "password";
          $(".icon-eyes").removeClass("toggle-password");
        }
      },
      signin() {

      },
      enter() {
      },

      // showModal() {
      //   this.isModalVisible = true;
      // },
      // closeModal() {
      //   this.isModalVisible = false;
      // },

      //登入邏輯
      loginSubmit(){
        // 尚未輸入帳號
        if (this.username ==='') {
          console.log('>>',this.username)
          this.submitErrMsg = '尚未輸入帳號';
          // $("#myModal").remove();
          return;
        }
        // 尚未輸入密碼
        if (this.password ==='') {
          this.submitErrMsg  = '尚未輸入密碼';
          $("#myModal").remove();
          return;
        }
        if (this.username ==='' || this.password ==='' && this.username !=='a' || this.password!=='a') {
          // 錯誤訊息
          this.submitError = true;
          this.submitErrMsg = '帳號或密碼輸入錯誤';

        } else if (this.username ==='0910123123' && this.password==='a1s2D3f59') { 
          // success
          this.submitError = true;
          this.submitErrMsg = '登入成功';
          $("#myModal").remove();
        //   // 登入成功跳轉內頁
        //   this.$router.push({
        //     path: '/',
        //     query: { username: this.user.username }
        //   })
        }
      }
   

    },
    //BEGIN--生命週期
    beforeCreate: function() {
      //實體初始化
    },
    created: function() {
      //實體建立完成。資料 $data 已可取得，但 $el 屬性還未被建立。
  
    },
    beforeMount: function() {
      //執行元素掛載之前。
    },
    mounted: function() {
      //元素已掛載， $el 被建立。
    },
    beforeUpdate: function() {
      //當資料變化時被呼叫，還不會描繪 View。
    },
    updated: function() {
      //當資料變化時被呼叫，還不會描繪 View。
    },
    beforeDestroy: function() {
      //實體還可使用。
    },
    destroyed: function() {
      //實體銷毀。
    }
    //END--生命週期
  }
  </script>