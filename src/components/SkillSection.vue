<template>
    <!-- 🛠️ My Skills 섹션 -->
    <section class="py-10">
        <h2 class="text-h4 font-weight-bold mb-6">🛠️ My Skills</h2>

        <v-row>
            <!-- 🔧 스킬 카드 반복 렌더링 -->
            <v-col v-for="(skill, index) in skills" :key="index" cols="6" sm="6" md="3">
                <v-card class="pa-4 skill-card h-100 d-flex flex-column justify-space-between" elevation="2" :class="[
                    `border-hover-${skill.hoverColor || skill.color}`,
                    ['Vue', 'React', 'Python'].includes(skill.name) ? 'learning-card' : ''
                ]">
                    <!-- 🏷️ 학습중 뱃지 -->
                    <v-chip v-if="['Vue', 'React', 'Python'].includes(skill.name)" class="ml-auto mb-2 learning-chip"
                        size="x-small" color="#F44336" text-color="white" label>
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
            </v-col>

        </v-row>
    </section>
</template>

<script>
export default {
    data() {
        return {
            // 🧠 나의 기술 스택
            skills: [
                {
                    name: "Photoshop",
                    icon: "mdi-image",
                    desc: "이미지 보정과 합성 작업",
                    color: "indigo",
                    colorCode: "#3f51b5",
                },
                {
                    name: "Illustrator",
                    icon: "mdi-vector-square",
                    desc: "벡터 기반 일러스터 제작",
                    color: "deep-orange",
                    colorCode: "#ff5722",
                },
                {
                    name: "Figma",
                    icon: "mdi-palette",
                    desc: "웹/App UI 화면 구성과 프로토타입 제작",
                    color: "figma",
                    colorCode: "#A259FF",
                },
                {
                    name: "Ae + Pr",
                    icon: "mdi-movie-open",
                    desc: "모션그래픽 및 영상 편집",
                    color: "deep-purple",
                    colorCode: "#673ab7",
                },
                {
                    name: "HTML",
                    icon: "mdi-language-html5",
                    desc: "접근성 고려한 구조적 웹 페이지 마크업",
                    color: "orange",
                    colorCode: "#ff9800",
                },
                {
                    name: "CSS",
                    icon: "mdi-language-css3",
                    desc: "스타일링 및 반응형 레이아웃 구현",
                    color: "blue",
                    colorCode: "#2196f3",
                },
                {
                    name: "SCSS",
                    icon: "mdi-sass",
                    desc: "유지보수에 유리한 스타일 구조 설계",
                    color: "pink",
                    colorCode: "#cc6699",
                },
                {
                    name: "Bootstrap",
                    icon: "mdi-bootstrap",
                    desc: "일관성 있는 컴포넌트 기반 UI 구축",
                    color: "purple",
                    colorCode: "#7952b3",
                },
                {
                    name: "Vue",
                    icon: "mdi-vuejs",
                    desc: "유연한 UI와 재사용 가능한 설계",
                    color: "green",
                    colorCode: "#4caf50",
                },
                {
                    name: "React",
                    icon: "mdi-react",
                    desc: "SPA 구조와 상태 관리 학습중",
                    color: "blue",
                    hoverColor: "react-blue",
                    colorCode: "#61DAFB",
                },
                {
                    name: "Python",
                    icon: "mdi-language-python",
                    desc: "데이터 처리와 자동화 기초 학습중",
                    color: "cyan",
                    colorCode: "#00bcd4",
                },
            ],
        };
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
}

/* 🌈 호버 시 테두리 색상 */
.border-hover-indigo:hover {
    border-color: #3f51b5;
}

.border-hover-deep-orange:hover {
    border-color: #ff5722;
}

.border-hover-figma:hover {
    border-color: #A259FF;
}

.border-hover-deep-purple:hover {
    border-color: #673ab7;
}

.border-hover-orange:hover {
    border-color: #ff9800;
}

.border-hover-blue:hover {
    border-color: #2196f3;
}

.border-hover-pink:hover {
    border-color: #cc6699;
}

.border-hover-purple:hover {
    border-color: #7952b3;
}

.border-hover-green:hover {
    border-color: #4caf50;
}

.border-hover-react-blue:hover {
    border-color: #61DAFB;
}

.border-hover-cyan:hover {
    border-color: #00bcd4;
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
</style>
