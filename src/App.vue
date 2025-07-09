<template>
  <v-app>
    <!-- 📌 상단 AppBar -->
    <v-app-bar app color="#4F5D75" dark dense flat>
      <v-toolbar-title class="font-weight-bold mr-8" @click="scrollToTop" style="cursor: pointer">
        YEON
      </v-toolbar-title>

      <!-- 📁 탭 메뉴 -->
      <v-tabs v-model="selectedTab" background-color="transparent" align-tabs="start" class="flex-grow-1" show-arrows
        slider-color="white">
        <v-tab class="nav-tab" @click="navigateAndScroll('about')">👩‍🎨 소개</v-tab>
        <v-tab class="nav-tab" @click="navigateAndScroll('skills')">🛠️ 스킬</v-tab>
        <v-tab class="nav-tab" @click="navigateAndScroll('projects')">📁 프로젝트</v-tab>
        <v-tab class="nav-tab" @click="navigateAndScroll('contact')">📬 연락처</v-tab>
      </v-tabs>
    </v-app-bar>

    <!-- 📝 본문 영역 -->
    <v-main>
      <router-view />
    </v-main>

    <!-- ⬆️ Top 버튼 (조건부 표시) -->
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
/* 📐 섹션 상단 여백 확보 */
[id] {
  scroll-margin-top: 100px;
}

/* 🖌️ 탭 메뉴 폰트 */
.nav-tab {
  font-family: 'SUITE-Bold', sans-serif;
  font-weight: 700;
  letter-spacing: -0.3px;
}

/* ⬆️ Top 버튼 스타일 */
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
