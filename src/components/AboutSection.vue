<template>
    <!-- 🙋‍♀️ About Me 섹션 -->
    <section class="py-10">
        <h2 class="text-h4 font-weight-bold mb-8">
            🙋‍♀️ About Me
        </h2>

        <v-container>
            <v-row>
                <!-- 👤 인사 및 해시태그 -->
                <v-col cols="12" md="6">
                    <div class="d-flex align-center mb-4">
                        <v-img src="/image/memoji.png" max-width="150" class="mr-4" alt="지연 미모티콘" />
                        <div>
                            <p class="text-body-2 font-weight-medium mb-1" style="color: #4F5D75;">
                                디자인과 구현을 함께 공부하는 웹 디자이너입니다.
                            </p>
                            <h3 class="font-weight-bold mb-2">
                                안녕하세요! <span style="color: #2C3E50;">지연</span>입니다 🐧
                            </h3>
                            <p class="mb-1">
                                디자인과 코드 사이에서<br />
                                <strong style="color: #2C3E50;">정돈된 화면</strong>을 만드는 걸 좋아해요.
                            </p>
                        </div>
                    </div>

                    <!-- 🏷️ 해시태그 키워드 -->
                    <v-row class="ml-1" dense>
                        <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#정리</v-chip>
                        <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#디테일</v-chip>
                        <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#정돈</v-chip>
                        <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#꼼꼼</v-chip>
                        <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#질서</v-chip>
                        <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#배려</v-chip>
                        <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#균형</v-chip>
                    </v-row>
                </v-col>

                <!-- 💡 성향 및 특징 리스트 -->
                <v-col cols="12" md="6">
                    <v-list dense>
                        <v-list-item>
                            <v-list-item-icon>
                                <v-icon color="#2C3E50">mdi-format-list-bulleted-square</v-icon>
                            </v-list-item-icon>
                            <v-list-item-content>
                                <v-list-item-title class="multiline-title">
                                    복잡한 내용을 <strong style="color: #2C3E50;">깔끔하게</strong> 정리하는 걸 좋아해요
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>

                        <v-list-item>
                            <v-list-item-icon>
                                <v-icon color="#2C3E50">mdi-eye-outline</v-icon>
                            </v-list-item-icon>
                            <v-list-item-content>
                                <v-list-item-title class="multiline-title">
                                    눈에 띄진 않아도 <strong style="color: #2C3E50;">자연스럽게</strong> 이어지는 구조를 좋아해요
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>

                        <v-list-item>
                            <v-list-item-icon>
                                <v-icon color="#2C3E50">mdi-code-tags</v-icon>
                            </v-list-item-icon>
                            <v-list-item-content>
                                <v-list-item-title class="multiline-title">
                                    <strong style="color: #2C3E50;">HTML / CSS / Vue</strong>로 실제 화면도 구현합니다
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>

                        <v-list-item>
                            <v-list-item-icon>
                                <v-icon color="#2C3E50">mdi-pencil</v-icon>
                            </v-list-item-icon>
                            <v-list-item-content>
                                <v-list-item-title class="multiline-title">
                                    완성도와 <strong style="color: #2C3E50;">디테일</strong>을 챙기고,
                                    부족한 부분은 <strong style="color: #2C3E50;">계속 배워서 채워요</strong>
                                </v-list-item-title>
                            </v-list-item-content>
                        </v-list-item>
                    </v-list>
                </v-col>
            </v-row>
        </v-container>
    </section>
</template>

<style scoped>
/* 📌 섹션 타이틀에 SUITE-Bold 폰트 적용 */
h2.text-h4 {
    font-family: 'SUITE-Bold', sans-serif;
    font-weight: 700;
}

/* 📝 리스트 항목: 줄바꿈 가능하게 */
.multiline-title {
    white-space: normal;
    overflow: visible;
    text-overflow: unset;
}

/* 리스트 전체에 줄바꿈 허용 */
.v-list-item-content {
    white-space: normal;
}
</style>
