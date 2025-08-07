<template>
  <v-app>
    <!-- 상단 AppBar -->
    <v-app-bar app color="#4F5D75" dark dense flat>

      <!-- v-toolbar-title -->
      <v-toolbar-title class="pl-5 pr-0 d-none d-md-flex" @click="scrollToTop" style="cursor: pointer; margin: 0;">
        <v-img src="/image/yeon-2.png" alt="YEON 로고" contain height="50" width="auto" class="ma-0" />
      </v-toolbar-title>

      <!-- 탭 메뉴 -->
      <div class="tab-wrapper-center">
        <v-tabs v-model="selectedTab" background-color="transparent" align-tabs="center" slider-color="white"
          class="tab-bar-center">
          <v-tab class="nav-tab" @click="navigateAndScroll('about')">👩🏻‍💻 소개</v-tab>
          <v-tab class="nav-tab" @click="navigateAndScroll('skills')">🛠️ 스킬</v-tab>
          <v-tab class="nav-tab" @click="navigateAndScroll('projects')">📁 프로젝트</v-tab>
          <v-tab class="nav-tab" @click="navigateAndScroll('contact')">📬 연락처</v-tab>
        </v-tabs>
      </div>
    </v-app-bar>


    <!-- 본문 영역 -->
    <v-main>
      <router-view />
    </v-main>

    <!-- Top 버튼 -->
    <v-btn v-show="showTopBtn" class="back-to-top-glass" elevation="3" icon @click="scrollToTop">
      <v-icon color="white">mdi-chevron-up</v-icon>
    </v-btn>


  </v-app>
</template>

<script>
export default {
  data() {
    return {
      selectedTab: null,
      showTopBtn: false,
    };
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    },
    navigateAndScroll(id) {
      if (this.$route.path !== '/') {
        this.$router.push({ path: '/', query: { scrollTo: id } });
      } else {
        this.scrollToSection(id);
      }
    },
    scrollToSection(id) {
      this.$nextTick(() => {
        const el = document.getElementById(id);
        if (el) el.scrollIntoView({ behavior: 'smooth' });
      });
    },
    handleScroll() {
      this.showTopBtn = window.scrollY > 300;
    },
  },
  watch: {
    '$route.query.scrollTo'(val) {
      if (val) this.scrollToSection(val);
    },
  },
};
</script>

<style scoped>
/* 섹션 상단 여백 확보 */
[id] {
  scroll-margin-top: 100px;
}

/* 상단 메뉴 중앙정렬 */
.tab-wrapper-center {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1;
}

.tab-bar-center {
  min-width: max-content;
}

/* 탭 메뉴 폰트 */
.nav-tab {
  font-family: 'SUITE-Bold', sans-serif;
  font-weight: 700;
  letter-spacing: -0.3px;
}

/* Top 버튼 스타일 */
.back-to-top-glass {
  position: fixed;
  bottom: 28px;
  right: 28px;
  backdrop-filter: blur(6px);
  background-color: rgba(79, 93, 117, 0.6);
  transition: background-color 0.3s ease;
  z-index: 999;
}

.back-to-top-glass:hover {
  background-color: rgba(79, 93, 117, 0.9);
}
</style>
