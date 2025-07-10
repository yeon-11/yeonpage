<template>
    <!-- 📬 Contact 섹션 -->
    <v-container fluid class="py-16 contact-section">
        <v-row justify="center">
            <v-col cols="12" md="8" lg="6" class="text-center">
                <!-- ✉️ 헤더 -->
                <v-icon size="48" color="#4F5D75" class="mb-2">mdi-email-outline</v-icon>
                <!-- 데스크탑용 문구 -->
                <h5 class="text-h5 font-weight-bold mb-3 d-none d-sm-block">
                    궁금한 점이 있다면 편하게 메시지를 보내주세요
                </h5>
                <!-- 모바일용 문구 -->
                <h5 class="text-h5 font-weight-bold mb-3 d-sm-none">
                    궁금한 점이 있다면<br>편하게 메시지를 보내주세요
                </h5>
                <p>연락을 기다리고 있겠습니다! 💬</p>

                <!-- 🔗 연락 아이콘 + 라벨 -->
                <div class="mt-8 contact-icons">
                    <div class="text-center">
                        <v-btn icon href="sms:01091574660" class="icon-hover">
                            <v-icon size="28">mdi-chat</v-icon>
                        </v-btn>
                        <div class="caption mt-5">문자 보내기</div>
                    </div>

                    <div class="text-center">
                        <v-btn icon href="mailto:wldus4660@naver.com" class="icon-hover">
                            <v-icon size="28">mdi-email</v-icon>
                        </v-btn>
                        <div class="caption mt-5">이메일 보내기</div>
                    </div>

                    <div class="text-center">
                        <v-btn icon href="https://github.com/yeon-11" target="_blank" class="icon-hover">
                            <v-icon size="28">mdi-github</v-icon>
                        </v-btn>
                        <div class="caption mt-5">코드 보러가기</div>
                    </div>
                </div>
            </v-col>
        </v-row>
    </v-container>
</template>

<style scoped>
/* 🖌️ 폰트 적용: 헤더 + 라벨 */
.contact-section h5,
.contact-section .caption {
    font-family: 'SUITE-Regular', sans-serif;
}

/* 📌 연락 아이콘 컨테이너 */
.contact-icons {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 100px;
    flex-wrap: nowrap;
}

/* 📱 모바일(화면 너비 600px 이하)에서 세로 정렬 */
@media (max-width: 600px) {
    .contact-icons {
        gap:30px;
    }
}

/* ✨ 버튼 호버 애니메이션 */
.contact-icons v-btn {
    transition: transform 0.2s ease;
}

.contact-icons v-btn:hover {
    transform: scale(1.15);
}

/* 🎵 아이콘 흔들 효과 */
.icon-hover .v-icon {
    transition: color 0.2s ease;
}

.icon-hover:hover .v-icon {
    color: #4f5d75;
    animation: shake 0.5s ease-in-out;
}

/* 🎵 흔들림 키프레임 */
@keyframes shake {
    0% {
        transform: rotate(0deg);
    }

    20% {
        transform: rotate(-10deg);
    }

    40% {
        transform: rotate(10deg);
    }

    60% {
        transform: rotate(-6deg);
    }

    80% {
        transform: rotate(6deg);
    }

    100% {
        transform: rotate(0deg);
    }
}
</style>
