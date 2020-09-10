<template>
  <v-app>
    <v-app-bar app dark top tag="header">
      <v-app-bar-nav-icon @click="draw = !draw"></v-app-bar-nav-icon>
      <v-toolbar-title>vuetify-연습</v-toolbar-title>
      <v-spacer />
      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
      <v-btn color="primary" outlined @click="dialog = true" v-if="loginUser == null">로그인</v-btn>
      <v-toolbar-items v-if="loginUser != null">
        <v-list-item dense>
          <v-list-item-avatar>
            <v-img src="https://cdn.vuetifyjs.com/images/john.png"></v-img>
          </v-list-item-avatar>
          <v-list-item-content>
            <v-list-item-title>유저 이름</v-list-item-title>
            <v-list-item-subtitle>유저 나이asd</v-list-item-subtitle>
          </v-list-item-content>
          <v-btn color="error" outlined @click="logout">Logout</v-btn>
        </v-list-item>
      </v-toolbar-items>
    </v-app-bar>
    <!-- nav -->
    <v-navigation-drawer v-model="draw" absolute temporary dark>
      <v-list-item two-line dense>
        <v-list-item-content>
          <v-list-item-title class="font-weight-bold text-lg-h6 text-center">LOGO</v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider />

      <!-- 유저 기록 -->
      <v-expansion-panels v-if="loginUser != null">
        <v-expansion-panel>
          <v-expansion-panel-header>
            <v-list-item>
              <v-list-item-avatar>
                <v-img
                  src="https://avatars2.githubusercontent.com/u/67082137?s=460&u=f69e0bb8fbf80e5c67c541ae99bd4868100a5e17&v=4"
                ></v-img>
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title>유저 이름</v-list-item-title>
                <v-list-item-subtitle>로그인중 입니다.</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-list>
              <v-list-item v-for="item in userItems" :key="item.title" link>
                <v-list-item-icon>
                  <v-icon>{{ item.icon }}</v-icon>
                </v-list-item-icon>
                <v-list-item-content>{{ item.title }}</v-list-item-content>
              </v-list-item>
            </v-list>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>

      <v-divider />

      <v-list rounded>
        <v-list-item-group>
          <v-list-item v-for="item in drawItems" :key="item.title" link>
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <!-- 로그인 팝업 -->
    <v-dialog dark min-width="380px" max-width="500px" v-model="dialog" v-if="loginUser == null">
      <v-card>
        <v-card-title class="headline">로그인 창</v-card-title>
        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              label="Account"
              v-model="account"
              prepend-icon="mdi-account"
              type="text"
              color="light-blue lighten-2"
              :rules="accountRules"
              :counter="10"
              outlined
              required
            ></v-text-field>
            <v-text-field
              label="Password"
              v-model="pass"
              prepend-icon="mdi-lock"
              type="password"
              color="light-blue lighten-2"
              outlined
              :rules="passwordRules"
              required
            ></v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="light-blue accent-2" outlined :disabled="!valid" @click="loginProcess">로그인</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-main>
      <v-card
        max-width="200"
        max-height="250"
        class="d-inline-block mx-auto ma-6"
        color="grey lighten-3"
        v-for="(movie, i) in movieInfo"
        :key="i"
      >
        <v-container>
          <v-img width="180" height="220" :src="movie.image">
            <v-chip class="my-chip ma-2" color="purple" label text-color="white" small>
              <v-icon left small>mdi-label</v-icon>
              {{ movie.genre }}
            </v-chip>
          </v-img>
        </v-container>
        <v-card-title>{{ movie.title }}</v-card-title>
        <v-card-subtitle>{{ movie.date }}</v-card-subtitle>
        <v-card-text>
          <v-rating :value="movie.rating" dense color="amber" size="14" half-increments readonly></v-rating>
          <span>({{ movie.rating }})</span>
          <strong>(120)</strong>
        </v-card-text>
      </v-card>
      <router-view />
    </v-main>

    <v-footer dark absolute height="60px" padless>
      <v-spacer></v-spacer>
      {{ new Date().getFullYear() }} —
      <strong>Jimin</strong>
    </v-footer>
  </v-app>
</template>

<script>
// import LoginPop from '@/components/LoginCom';
export default {
  name: "App",
  components: {
    // LoginPop
  },
  data: () => ({
    loginUser: null,
    account: "",
    pass: "",
    valid: false,
    draw: null,
    drawItems: [
      { title: "Home", icon: "mdi-home-city" },
      { title: "Movie", icon: "mdi-movie" },
      { title: "게시판", icon: "mdi-forum" },
    ],
    userItems: [
      { title: "유저 정보 확인", icon: "mdi-account" },
      { title: "내가 본 영화목록", icon: "mdi-movie-search" },
      { title: "보고싶은 영화", icon: "mdi-bookmark-check" },
    ],
    dialog: false,
    accountRules: [
      (v) => !!v || "아이디를 입력하세요",
      (v) => v.length <= 10 || "아이디는 10글자 이내로만 작성 가능합니다.",
    ],
    passwordRules: [(v) => !!v || "비밀번호를 입력하세요"],
    movieInfo: [
      {
        title: "공포분자",
        image:
          "https://movie-phinf.pstatic.net/20200728_227/1595916020037z3gR6_JPEG/movie_image.jpg?type=m203_290_2",
        date: "2020",
        genre: "공포",
        rating: 3.4,
      },
      {
        title: "007노 타임 투 다이",
        image:
          "https://movie-phinf.pstatic.net/20200305_156/1583390851443dK953_JPEG/movie_image.jpg?type=m203_290_2",
        date: "2020",
        genre: "액션",
        rating: 3.4,
      },
    ],
  }),
  methods: {
    loginProcess() {
      this.loginCheck();
      this.axios.get("/").then((res) => {
        console.log(res);
      });
    },
    loginCheck() {
      let check = this.$refs.form.validate();
      if (check) {
        this.$refs.form.reset();
        this.account = "";
        this.pass = "";
        this.dialog = false;
        this.loginUser = "로그인중";
      }
    },
    logout() {
      this.loginUser = null;
    },
  },
};
</script>

<style scoped>
.my-chip {
  position: absolute;
  bottom: 0;
}
</style>
