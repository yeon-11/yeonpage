<template>
    <!-- 🙋‍♀️ About Me 섹션 -->
    <section>
        <h2 class="text-h4 font-weight-bold mb-8">
            🙋‍♀️ About Me
        </h2>

        <v-container>
            <v-row>
                <v-col cols="12">
                    <div class="about-wrapper">
                        <!-- 👤 프로필 이미지 -->
                        <v-img src="/public/image/memoji.png" class="profile-image" alt="지연 미모티콘" contain />

                        <!-- 💬 소개 텍스트 + 해시태그 -->
                        <div class="about-info">
                            <div class="about-text">
                                <p class="text-body-2 font-weight-medium mb-1" style="color: #4F5D75;">
                                    디자인과 구현을 함께 공부하는 웹 디자이너입니다.
                                </p>
                                <h3 class="font-weight-bold mb-2">
                                    안녕하세요! <span style="color: #2C3E50;">지연</span>입니다 🐧
                                </h3>
                                <p class="mb-4">
                                    디자인과 코드 사이에서<br />
                                    <strong style="color: #2C3E50;">정돈된 화면</strong>을 만드는 걸 좋아해요.
                                </p>
                            </div>

                            <!-- 🏷️ 해시태그 키워드 -->
                            <v-row class="about-tags mb-5" dense>
                                <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#정리</v-chip>
                                <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#정돈</v-chip>
                                <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#디테일</v-chip>
                                <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#꼼꼼</v-chip>
                                <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#질서</v-chip>
                                <v-chip class="ma-1" variant="outlined" color="#4F5D75" label>#균형</v-chip>
                            </v-row>
                        </div>
                    </div>
                </v-col>


                <!-- 💡 성향 및 특징 리스트 -->
                <v-row dense>
                    <v-col cols="12" sm="6">
                        <div class="feature-item">
                            <v-icon color="#2C3E50" class="mr-2">mdi-format-list-bulleted-square</v-icon>
                            <span>복잡한 내용을 <strong style="color:#2C3E50;">깔끔하게</strong> 정리하는 걸 좋아해요</span>
                        </div>
                    </v-col>

                    <v-col cols="12" sm="6">
                        <div class="feature-item">
                            <v-icon color="#2C3E50" class="mr-2">mdi-eye-outline</v-icon>
                            <span>눈에 띄진 않아도 <strong style="color:#2C3E50;">자연스럽게</strong> 이어지는 구조를 좋아해요</span>
                        </div>
                    </v-col>

                    <v-col cols="12" sm="6">
                        <div class="feature-item">
                            <v-icon color="#2C3E50" class="mr-2">mdi-code-tags</v-icon>
                            <span><strong style="color:#2C3E50;">HTML / CSS / Vue</strong>로 실제 화면도 구현합니다</span>
                        </div>
                    </v-col>

                    <v-col cols="12" sm="6">
                        <div class="feature-item">
                            <v-icon color="#2C3E50" class="mr-2">mdi-pencil</v-icon>
                            <span>완성도와 <strong style="color:#2C3E50;">디테일</strong>을 챙기고, 부족한 부분은 <strong
                                    style="color:#2C3E50;">계속 배워서 채워요</strong></span>
                        </div>
                    </v-col>
                </v-row>

            </v-row>
        </v-container>
    </section>
</template>

<style scoped>
/* 📌 섹션 타이틀 - SUITE-Bold 폰트 적용 */
h2.text-h4 {
    font-family: 'SUITE-Bold', sans-serif;
    font-weight: 700;
}

/* 📝 리스트 항목: 줄바꿈 허용 */
.multiline-title {
    white-space: normal;
    overflow: visible;
    text-overflow: unset;
}

/* 🧾 리스트 전체에 줄바꿈 허용 */
.v-list-item-content {
    white-space: normal;
}

/* 👤 About Me 전체 컨테이너 */
.about-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 24px;
    text-align: center;
}

/* 🎯 성향 항목 레이아웃 */
.feature-item {
    display: flex;
    align-items: flex-start;
    gap: 8px;
    margin-bottom: 16px;
    font-size: 0.95rem;
    line-height: 1.5;
}

/* 💬 텍스트 & 태그 포함 영역 */
.about-info {
    max-width: 100%;
}

/* 💬 텍스트 블럭 */
.about-text {
    margin-top: 0;
}

/* 🖼️ 이미지 */
.profile-image {
    width: 100%;
    max-width: 200px;
    margin: 0 auto;
}

/* 🏷️ 태그 칩 감싸는 영역 */
.about-tags {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 8px;
    max-width: 250px;
    margin: 8px auto 20px auto;
}

/* 각 칩에 크기 제한 (Vuetify v-chip은 기본 min-width가 커서 너비 제한 필요) */
.about-tags .v-chip {
    flex: 0 1 auto;
    max-width: calc(50% - 12px);
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    font-size: 0.85rem;
    padding: 0 8px;
}

/* 💻 패드 이상: 좌우 정렬 전환 */
@media (min-width: 601px) {
    .about-wrapper {
        flex-direction: row;
        text-align: left;
    }

    .about-info {
        flex: 1;
    }

    .about-tags {
        justify-content: flex-start;
        max-width: none;
        margin-left: 0;
        margin-right: 0;
    }

    .about-tags .v-chip {
        max-width: none;
    }
}
</style>
