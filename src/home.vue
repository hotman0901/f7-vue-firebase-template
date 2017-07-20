<template>
  <div id="app">
    <!-- 登入視窗，一開始狀態是隱藏的，使用js開啟他 -->
    <f7-login-screen id="loginScreen">
      <f7-view>
        <f7-pages>
          <f7-page login-screen>
            <f7-login-screen-title>Twitter Vue</f7-login-screen-title>
            <!-- <img src="../gfx/tweetLogo.png" alt="" id="tweetLogo">  -->
            <f7-list>
              <f7-list-button title="Sign In"></f7-list-button>
              <f7-list-label>
                <p>Click Sign In to log in to Twitter</p>
              </f7-list-label>
            </f7-list>
            <!-- list-block-label 是有text-align:center -->
            <div class="list-block-label">
              <p>
                <a href="#" class="close-login-screen">Close Login Screen</a>
              </p>
            </div>
          </f7-page>
        </f7-pages>
      </f7-view>
    </f7-login-screen>
    <!-- 主畫面 -->
    <f7-views navbar-through="">
      <f7-view main="" url="/" :dynamic-navbar="true">
        <f7-navbar>
          <f7-nav-left></f7-nav-left>
          <f7-nav-center sliding="">CHUBSH-IG</f7-nav-center>
          <f7-nav-right></f7-nav-right>
        </f7-navbar>
        <f7-pages id="pages">
          <f7-page>
            <!-- <f7-list>
              <f7-list-item title="To page 1" link="/login/"></f7-list-item>
              <f7-list-item title="To page 2" link="/page2/"></f7-list-item>
            </f7-list> -->
            <!-- <f7-buttons> -->
              <!-- 開啟login的modal，不是換頁 -->
              <!-- <f7-button @click="openlogin">login</f7-button> -->
              <!-- <f7-link href="/login/">Login</f7-link> -->
              <!-- <f7-button @click="logout">logout</f7-button> -->
            <!-- </f7-buttons> -->
            <!-- content-block 左右 padding 15px -->
            <div class="content-block">
              <img src="./assest/img/tweetLogo.png" alt="" id="tweetLogo"> 
              <p>
                <a href="#" class="button button-big button-fill color-black">Login</a>
              </p>
            </div>
          </f7-page>
        </f7-pages>
      </f7-view>
    </f7-views>
  
  </div>
</template>

<script>
import firebase from 'firebase';
import firebaseData from './firebase/firebasedata';

let vm;
export default {
  name: 'app',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App with Framework7 and Webpack'
    }
  }, created() {
    vm = this;
    // 初始化，宣告成一個變數是之後可以拿來用
    firebase.initializeApp(firebaseData);
  }, methods: {
    closeLogin() {
      window.f7.closeModal();
    },
    openlogin() {
      window.f7.loginScreen();
    },
    logout() {
      firebase.auth().signOut().then(function () {
        // Sign-out successful.
        console.log('fb登出');
        // 因為這裡不能再呼叫其他方法所以都改在onAuthStateChanged去判斷
      }, function (error) {
        // An error happened.
        console.log('fb登出失敗');
      });
    },
    login() {
      var provider = new firebase.auth.FacebookAuthProvider();

      provider.setCustomParameters({
        'display': 'popup'
      });
      provider.addScope('email');
      provider.addScope('public_profile');
      // provider.addScope('user_birthday');
      firebase.auth().signInWithPopup(provider).then(function (result) {
        // This gives you a Facebook Access Token. You can use it to access the Facebook API.
        var token = result.credential.accessToken;
        // The signed-in user info.
        console.log("login");

        var user = result.user;
        console.log(user);
      }).catch(function (error) {
        console.log("login-error");
        // Handle Errors here.
        const errorCode = error.code;
        const errorMessage = error.message;
        console.log("errorCode:" + errorCode);
        console.log("errorMessage:" + errorMessage);
        // The email of the user's account used.
        const email = error.email;
        console.log("email:" + email);
        // The firebase.auth.AuthCredential type that was used.
        const credential = error.credential;
        console.log("credential:" + credential);
      });
    }
  }
}
</script>

<style lang="scss">
#tweetLogo{
  width: 20%;
}
</style>
