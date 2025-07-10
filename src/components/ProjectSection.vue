<template>
    <!-- 📁 Projects 섹션 -->
    <section class="py-10">
        <h2 class="text-h4 font-weight-bold mb-8">📁 Projects</h2>

        <v-row dense>
            <!-- 🖼️ 프로젝트 카드 반복 -->
            <v-col v-for="(project, index) in paginatedProjects" :key="index" cols="12" sm="6" md="4" class="mb-3">
                <v-card class="mx-auto equal-height" max-width="500">
                    <!-- ✅ 이미지 내부 패딩 주기 -->
                    <v-sheet class="pa-3" color="transparent" elevation="0" height="300px">
                        <v-img :src="project.image" height="100%" contain />
                    </v-sheet>

                    <v-card-title class="text-wrap">
                        <b>{{ project.title }}</b>
                    </v-card-title>

                    <v-card-text>
                        {{ project.description }}
                        <div class="mt-2 d-flex flex-wrap">
                            <v-chip v-for="(tool, i) in project.tools" :key="i" class="ma-1" :color="tool.color"
                                variant="outlined" size="small">
                                {{ tool.name }}
                            </v-chip>
                        </div>
                    </v-card-text>

                    <v-card-actions>
                        <v-btn v-if="project.github" :href="project.github" target="_blank" text>
                            <b>💻 작업물 보기</b>
                        </v-btn>
                        <v-btn v-else-if="project.pdf" :href="project.pdf" target="_blank" text>
                            <b>📄 작업물 보기</b>
                        </v-btn>
                    </v-card-actions>
                </v-card>
            </v-col>
        </v-row>

        <!-- 📄 페이지네이션 -->
        <v-row justify="center" class="mt-8">
            <v-pagination v-model="currentPage" :length="pageCount" :total-visible="5" />
        </v-row>
    </section>
</template>

<script>
export default {
    name: "ProjectSection",
    data() {
        const base = import.meta.env.BASE_URL; // ✅ base 경로 추출

        return {
            currentPage: 1,
            itemsPerPage: 6,
            // 🗂️ 프로젝트 목록 데이터
            projects: [
                {
                    title: "PLANLOG",
                    description: "편리한 To Do List 앱 UI를 포토샵으로 제작.",
                    tools: [
                        { name: "Photoshop", color: "indigo" },
                        { name: "HTML", color: "orange" },
                        { name: "CSS", color: "blue" },
                    ],
                    image: base + "image/planlog.png",
                    github: "https://yeon-11.github.io/planlog/",
                },
                {
                    title: "그대안의블루",
                    description: "청년 우울증의 원인과 해결 방법을 카드뉴스로 제작.",
                    tools: [
                        { name: "Illustrator", color: "deep-orange" },
                    ],
                    image: base + "image/the_blue_inside_you.png",
                    pdf: base + "image/the_blue_inside_you.pdf",
                },
                {
                    title: "SUBWAY",
                    description: "서브웨이의 신선함을 일러스트와 에펙으로 표현.",
                    tools: [
                        { name: "Illustrator", color: "deep-orange" },
                        { name: "After Effects", color: "deep-purple" },
                        { name: "HTML", color: "orange" },
                        { name: "CSS", color: "blue" },
                    ],
                    image: base + "image/subway.png",
                    github: "https://yeon-11.github.io/subway-advertising/",
                },
                {
                    title: "addct",
                    description: "기존 홈페이지를 나만의 스타일로 리디자인.",
                    tools: [
                        { name: "HTML", color: "orange" },
                        { name: "CSS", color: "blue" },
                        { name: "Bootstrap", color: "purple" },
                    ],
                    image: base + "image/addct.png",
                    github: "https://yeon-11.github.io/addct-redesign/",
                },
                {
                    title: "Antenna",
                    description: "안테나의 음악 철학을 재해석하여 리디자인한 프로젝트.",
                    tools: [
                        { name: "HTML", color: "orange" },
                        { name: "CSS", color: "blue" },
                        { name: "SCSS", color: "pink" },
                    ],
                    image: base + "image/antenna.png",
                    github: "https://yeon-11.github.io/antenna-redesign/",
                },
                {
                    title: "미드림성형외과",
                    description: "오래된 사이트를 요즘 스타일로 리디자인한 프로젝트.",
                    tools: [
                        { name: "Vue", color: "green" },
                        { name: "CSS", color: "blue" },
                        { name: "SCSS", color: "pink" },
                        { name: "Figma", color: "#A259FF" },
                    ],
                    image: base + "image/meedream.png",
                    github: "https://yeon-11.github.io/meedream-redesign/",
                },
                // {
                //   title: "React 미니 블로그",
                //   description: "React로 만든 CRUD 기능 블로그 애플리케이션.",
                //   tools: [
                //     { name: "HTML", color: "orange" },
                //     { name: "CSS", color: "blue" },
                //     { name: "React", color: "blue" },
                //   ],
                //   image: "https://via.placeholder.com/800x600?text=React+Blog",
                //   github: "https://yeon-11.github.io/",
                // },
                // {
                //   title: "Python 데이터 시각화",
                //   description: "Python으로 데이터를 시각화하고 Matplotlib으로 그래프 구현.",
                //   tools: [{ name: "Python", color: "cyan" }],
                //   image: "https://via.placeholder.com/800x600?text=Python+Visualization",
                //   github: "https://yeon-11.github.io/",
                // },
            ],
        };
    },
    computed: {
        // 📊 총 페이지 수 계산
        pageCount() {
            return Math.ceil(this.projects.length / this.itemsPerPage);
        },
        // 📌 현재 페이지 기준으로 보여줄 프로젝트 목록
        paginatedProjects() {
            const start = (this.currentPage - 1) * this.itemsPerPage;
            const end = start + this.itemsPerPage;
            return this.projects.slice(start, end);
        },
    },
    methods: {
        // 📱 화면 너비에 따라 itemsPerPage 조절 (모바일: 3개, 데스크탑: 6개)
        updateItemsPerPage() {
            const isMobile = window.innerWidth <= 600; // Vuetify 기준 sm 이하
            this.itemsPerPage = isMobile ? 3 : 6;
        }
    },
    mounted() {
        // ✅ 컴포넌트가 처음 로드될 때 사이즈 체크
        this.updateItemsPerPage();
        // ✅ 화면 크기 변경 시 반응하도록 이벤트 리스너 등록
        window.addEventListener('resize', this.updateItemsPerPage);
    },
    beforeUnmount() {
        // ✅ 메모리 누수 방지: 이벤트 리스너 제거
        window.removeEventListener('resize', this.updateItemsPerPage);
    }
};
</script>

<style scoped>
/* 🖌️ 섹션 타이틀 - SUITE-Bold 적용 */
h2.text-h4 {
    font-family: 'SUITE-Bold', sans-serif;
    font-weight: 700;
}

/* 📐 카드 높이 균일화 및 내부 정렬 */
.equal-height {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
}
</style>
