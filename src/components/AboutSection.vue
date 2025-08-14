<template>
    <section>
        <h2 class="text-h4 font-weight-bold mt-5 mb-15">👩🏻‍💻 About Me</h2>

        <v-container>
            <v-row class="about-wrapper" align="start">
                <!-- 프로필 이미지 -->
                <v-col cols="12" md="12" lg="4" class="text-center">
                    <v-img src="/public/image/memoji.png" class="profile-image" alt="지연 미모티콘" contain />
                </v-col>

                <!-- 소개 텍스트 + 해시태그 -->
                <v-col cols="12" md="6" lg="4">
                    <div class="about-info">
                        <p class="text-body-2 font-weight-medium mb-1" style="color: #4F5D75;">
                            디자인과 개발을 함께 배우고 있는 웹 디자이너
                        </p>
                        <h3 class="font-weight-bold mb-2">
                            안녕하세요, <span style="color: #E29500;">지연</span>입니다 🐧
                        </h3>
                        <p class="mb-4">
                            <strong style="color: #2C3E50;">깔끔하고 정돈된 화면</strong>을 만드는 걸 좋아하고,<br>
                            좋은 경험을 위해 계속 고민하고 배워가고 있어요.
                        </p>

                        <!-- 해시태그 -->
                        <v-row class="about-tags" dense>
                            <v-col v-for="(tag, i) in tags" :key="i" cols="3" md="auto"
                                class="d-flex justify-center pa-1">
                                <v-chip variant="outlined" color="#4F5D75" label>
                                    {{ tag }}
                                </v-chip>
                            </v-col>
                        </v-row>
                    </div>
                </v-col>

                <!-- 특징 리스트 -->
                <v-col cols="12" md="6" lg="4">
                    <div class="feature-list">
                        <div class="feature-item">
                            <v-icon color="#2C3E50" class="mr-2">mdi-format-list-bulleted-square</v-icon>
                            <span>복잡한 내용을 <strong style="color:#E29500;">깔끔하게</strong> 정리하는 걸 좋아해요</span>
                        </div>

                        <div class="feature-item">
                            <v-icon color="#2C3E50" class="mr-2">mdi-eye-outline</v-icon>
                            <span>눈에 띄지 않아도 <strong style="color:#2C3E50;">자연스럽게</strong> 이어지는 구조를 추구합니다</span>
                        </div>

                        <div class="feature-item">
                            <v-icon color="#2C3E50" class="mr-2">mdi-code-tags</v-icon>
                            <span><strong style="color:#2C3E50;">HTML / CSS / Vue</strong>로 구현하며 배우고 있어요</span>
                        </div>

                        <div class="feature-item">
                            <v-icon color="#2C3E50" class="mr-2">mdi-pencil</v-icon>
                            <span>
                                완성도와 <strong style="color:#E29500;">디테일</strong>을 중요하게 생각하고,<br>
                                부족한 부분은 <strong style="color:#2C3E50;">꾸준히 배워서</strong> 채워갑니다
                            </span>
                        </div>
                    </div>
                </v-col>
            </v-row>
        </v-container>
    </section>
</template>

<script>
export default {
    data() {
        return {
            tags: [
                "#정리", "#정돈", "#디테일",
                "#꼼꼼", "#질서", "#균형"
            ],
        };
    }
};
</script>

<style scoped>
/* 레이아웃 */
.about-wrapper {
    flex-wrap: wrap;
}

/* 프로필 이미지 */
.profile-image {
    max-width: 200px;
    margin: 0 auto;
}

/* 해시태그 스타일 */
.about-tags {
    display: flex;
    flex-wrap: wrap;
    justify-content: start;
    gap: 8px;
    margin-top: 12px;
}

.about-tags .v-chip {
    width: 100%;
    justify-content: center;
}

/* 특징 리스트 */
.feature-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
    padding-top: 8px;
}

.feature-item {
    display: flex;
    align-items: flex-start;
    font-size: 0.95rem;
    line-height: 1.5;
}

/* 모바일에서만 줄바꿈 */
.mb_only {
    display: none;
}

/* 📱 모바일 대응 */
@media (max-width: 600px) {
    .about-wrapper {
        flex-direction: column;
        align-items: center;
    }

    .feature-list {
        align-items: flex-start;
    }

    .mb_only {
        display: inline;
    }
}
</style>
