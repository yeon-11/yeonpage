<template>
    <!-- 🛠️ My Skills 섹션 -->
    <section class="py-15">
        <h2 class="text-h4 font-weight-bold mb-6">🛠️ My Skills</h2>

        <!-- 🌀 슬라이드형 스킬 그룹 -->
        <div class="skill-marquee" @mouseenter="pauseAnimation" @mouseleave="resumeAnimation" ref="marquee">
            <div class="skill-track" :class="{ paused: isPaused }">
                <div v-for="(skill, index) in [...skills, ...skills]" :key="index" class="skill-wrapper">
                    <v-card class="pa-4 skill-card d-flex flex-column justify-space-between" elevation="2" :class="[
                        `border-hover-${skill.hoverColor || skill.color}`,
                        ['Premiere Pro', 'Vue', 'React', 'Python'].includes(skill.name) ? 'learning-card' : ''
                    ]">
                        <!-- 🏷️ 학습중 뱃지 -->
                        <v-chip v-if="['Premiere Pro', 'Vue', 'React', 'Python'].includes(skill.name)"
                            class="learning-chip" size="x-small" color="#F44336" text-color="white" label
                            style="position: absolute; top: 8px; right: 8px; z-index: 2">
                            공부중
                        </v-chip>


                        <v-icon :style="{ color: skill.colorCode }" size="36" class="mb-2">
                            {{ skill.icon }}
                        </v-icon>
                        <v-card-title class="text-h6 font-weight-bold pa-0">
                            {{ skill.name }}
                        </v-card-title>
                        <v-card-text class="text-body-2 pa-0">
                            {{ skill.desc }}
                        </v-card-text>
                    </v-card>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            isPaused: false, // ⏸️ 애니메이션 일시정지 여부
            // 🧠 나의 기술 스택
            skills: [
                {
                    name: "Photoshop",
                    icon: "mdi-image",
                    desc: "이미지 보정과 합성 작업",
                    color: "ps-blue",
                    colorCode: "#31A8FF",
                },
                {
                    name: "Illustrator",
                    icon: "mdi-vector-square",
                    desc: "벡터 기반 일러스터 제작",
                    color: "ai-orange",
                    colorCode: "#FF9A00",
                },
                {
                    name: "Figma",
                    icon: "mdi-palette",
                    desc: "웹/App UI 화면 구성과 프로토타입 제작",
                    color: "figma-purple",
                    colorCode: "#A259FF",
                },
                {
                    name: "After Effects",
                    icon: "mdi-movie-open",
                    desc: "모션그래픽 및 시각 효과 제작",
                    color: "ae-purple",
                    colorCode: "#9999FF",
                },
                {
                    name: "Premiere Pro",
                    icon: "mdi-video-vintage",
                    desc: "영상 편집 및 컷 구성 작업",
                    color: "pr-purple",
                    colorCode: "#9999CC",
                },
                {
                    name: "HTML",
                    icon: "mdi-language-html5",
                    desc: "접근성 고려한 구조적 웹 페이지 마크업",
                    color: "html-orange",
                    colorCode: "#E34F26",
                },
                {
                    name: "CSS",
                    icon: "mdi-language-css3",
                    desc: "스타일링 및 반응형 레이아웃 구현",
                    color: "css-blue",
                    colorCode: "#1572B6",
                },
                {
                    name: "SCSS",
                    icon: "mdi-sass",
                    desc: "유지보수에 유리한 스타일 구조 설계",
                    color: "sass-pink",
                    colorCode: "#CD6799",
                },
                {
                    name: "Bootstrap",
                    icon: "mdi-bootstrap",
                    desc: "일관성 있는 컴포넌트 기반 UI 구축",
                    color: "bootstrap-purple",
                    colorCode: "#7952B3",
                },
                {
                    name: "Vue",
                    icon: "mdi-vuejs",
                    desc: "유연한 UI와 재사용 가능한 설계",
                    color: "vue-green",
                    colorCode: "#42B883",
                },
                {
                    name: "React",
                    icon: "mdi-react",
                    desc: "SPA 구조와 상태 관리 학습중",
                    color: "react-blue",
                    colorCode: "#61DAFB",
                },
                {
                    name: "Python",
                    icon: "mdi-language-python",
                    desc: "데이터 처리와 자동화 기초 학습중",
                    color: "python-blue",
                    colorCode: "#3776AB",
                },
            ],
        };
    },
    methods: {
        pauseAnimation() {
            this.isPaused = true;
        },
        resumeAnimation() {
            this.isPaused = false;
        },
    },
};
</script>

<style scoped>
/* 🖌️ 섹션 타이틀 - SUITE-Bold 적용 */
h2.text-h4 {
    font-family: 'SUITE-Bold', sans-serif;
    font-weight: 700;
}

/* 🧱 스킬 카드 내 폰트 통일 (SUITE-Regular) */
.skill-card,
.skill-card * {
    font-family: 'SUITE-Regular', sans-serif;
}

/* 🎨 스킬 카드 스타일 */
.skill-card {
    transition: border 0.3s ease;
    border: 2px solid transparent;
    border-radius: 8px;
    width: 200px;
    height: 160px;
    margin: 10px 0;
    box-sizing: border-box;
    flex-shrink: 0;
}

/* 🌈 호버 시 테두리 색상 */
.border-hover-ps-blue:hover {
    border-color: #31A8FF;
}

.border-hover-ai-orange:hover {
    border-color: #FF9A00;
}

.border-hover-figma-purple:hover {
    border-color: #A259FF;
}

.border-hover-ae-purple:hover {
    border-color: #9999FF;
}

.border-hover-pr-purple:hover {
    border-color: #9999CC;
}

.border-hover-html-orange:hover {
    border-color: #E34F26;
}

.border-hover-css-blue:hover {
    border-color: #1572B6;
}

.border-hover-sass-pink:hover {
    border-color: #CD6799;
}

.border-hover-bootstrap-purple:hover {
    border-color: #7952B3;
}

.border-hover-vue-green:hover {
    border-color: #42B883;
}

.border-hover-react-blue:hover {
    border-color: #61DAFB;
}

.border-hover-python-blue:hover {
    border-color: #3776AB;
}


/* 🧠 학습중 기술 회색 배경 */
.learning-card {
    background-color: #dadada;
}

/* 📛 학습중 뱃지에 강조 색상 */
.learning-chip {
    font-weight: bold;
    letter-spacing: 0.5px;
}

/* 🌀 슬라이드 설정 */
.skill-marquee {
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    display: flex;
    scrollbar-width: none;
}

.skill-marquee::-webkit-scrollbar {
    display: none;
}

.skill-track {
    display: flex;
    animation: scroll-marquee 30s linear infinite;
}

.skill-track.paused {
    animation-play-state: paused;
}

.skill-wrapper {
    flex: 0 0 auto;
    margin-right: 16px;
    scroll-snap-align: start;
}

@keyframes scroll-marquee {
    0% {
        transform: translateX(0);
    }

    100% {
        transform: translateX(-50%);
    }
}
</style>
