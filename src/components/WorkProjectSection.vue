<template>
    <v-container class="py-10 work-projects-section">
        <!-- 타이틀 -->
        <h2 class="text-h5 font-weight-bold mb-10">📂 Work Projects</h2>

        <!-- 준비중 문구 -->
        <!-- TODO: 실제 Work Projects 정리되면 이 영역에 리스트/카드 구조 다시 추가 -->
        <p class="text-body-2">
            🚧 업데이트 준비중 🚧 <br>
            조금만 기다려주세요:)
        </p>
    </v-container>
</template>

<script>
export default {
    name: "workProjects",
};
</script>

<style scoped>
/* 섹션 타이틀 - SUITE-Bold 적용 */
.work-projects-section h2 {
    font-family: "SUITE-Bold", sans-serif;
}

/* 본문 폰트 - SUITE-Regular 적용 */
.work-projects-section p {
    font-family: "SUITE-Regular", sans-serif;
}
</style>
