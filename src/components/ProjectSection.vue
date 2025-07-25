<template>
    <!-- Projects 섹션 -->
    <section class="py-15">
        <h2 class="text-h4 font-weight-bold mb-8">📁 Projects</h2>

        <!-- 카테고리 토글 버튼 -->
        <v-btn-toggle v-model="selectedCategory" class="mb-6" mandatory>
            <v-btn value="all">전체</v-btn>
            <v-btn value="design">디자인</v-btn>
            <v-btn value="video">모션·영상</v-btn>
            <v-btn value="web">웹 개발</v-btn>
        </v-btn-toggle>

        <!-- 프로젝트 카드 리스트 -->
        <v-row dense>
            <v-col v-for="(project, index) in paginatedProjects" :key="index" cols="12" sm="6" md="4" lg="4"
                class="mb-3">
                <!-- 프로젝트 카드 -->
                <v-card class="mx-auto equal-height" max-width="500">
                    <!-- 이미지 섹션 -->
                    <v-sheet class="pa-3" color="transparent" elevation="0" height="300px">
                        <v-img :src="project.image" height="100%" contain />
                    </v-sheet>

                    <!-- 타이틀 + 역할 -->
                    <v-card-title class="d-flex flex-column px-4 pt-4">
                        <v-chip v-if="project.type" color="grey lighten-2" text-color="black" size="small" label
                            class="mb-2 align-self-start">
                            {{ project.type }}
                        </v-chip>
                        <b class="text-wrap">{{ project.title }}</b>
                    </v-card-title>

                    <!-- 설명 및 툴 목록 -->
                    <v-card-text>
                        {{ project.description }}
                        <div class="mt-2 d-flex flex-wrap">
                            <v-chip v-for="(tool, i) in project.tools" :key="i" class="ma-1" :color="tool.color"
                                variant="outlined" size="small">
                                {{ tool.name }}
                            </v-chip>
                        </div>
                    </v-card-text>

                    <!-- 작업물 보기 버튼 -->
                    <v-card-actions>
                        <v-btn v-if="project.github" :href="project.github" target="_blank" text>
                            <b>💻 작업물 보기</b>
                        </v-btn>
                        <v-btn v-else-if="project.pdf" :href="project.pdf" target="_blank" text>
                            <b>📄 작업물 보기</b>
                        </v-btn>
                        <v-btn v-else-if="project.video || project.youtube" @click="openVideoModal(project)" text>
                            <b>🎥 작업물 보기</b>
                        </v-btn>
                    </v-card-actions>
                </v-card>
            </v-col>
        </v-row>

        <!-- 페이지네이션 -->
        <v-pagination v-if="pageCount > 1" v-model="currentPage" :length="pageCount"
            class="mt-6 d-flex justify-center" />

        <!-- 영상 모달 -->
        <v-dialog v-model="videoDialog" max-width="800px">
            <v-card>
                <v-card-title class="text-h6">🎥 {{ selectedTitle }} - 영상 보기</v-card-title>
                <v-card-text>
                    <video v-if="selectedVideo" :src="selectedVideo" controls autoplay
                        style="width: 100%; height: auto"></video>
                </v-card-text>
                <v-card-actions>
                    <v-spacer />
                    <v-btn text @click="videoDialog = false">닫기</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </section>
</template>

<script>
export default {
    name: "ProjectSection",
    watch: {
        selectedCategory() { // 카테고리 토글시 페이지 1 리셋
            this.currentPage = 1;
        },
    },

    data() {
        const base = import.meta.env.BASE_URL;
        return {
            selectedCategory: "all", // 선택된 프로젝트 카테고리
            videoDialog: false, // 영상 모달 열림 여부
            selectedVideo: null, // 선택된 영상 링크
            selectedTitle: "", // 영상 제목
            currentPage: 1, // 현재 페이지
            base, // 이미지 및 영상 경로 base
            projects: [
                {
                    title: "PLANLOG",
                    description: "할 일 관리에 최적화된 UI 디자인",
                    type: "기획 및 UI 디자인 중심 참여",
                    tools: [
                        { name: "Photoshop", color: "#31A8FF" },
                        { name: "HTML", color: "#E34F26" },
                        { name: "CSS", color: "#1572B6" },
                    ],
                    category: "design",
                    image: base + "image/planlog.png",
                    github: "https://yeon-11.github.io/planlog/",
                },
                {
                    title: "그대안의블루",
                    description: "청년 우울증을 주제로 한 카드뉴스 콘텐츠",
                    type: "특정 카드 디자인 참여",
                    tools: [
                        { name: "Illustrator", color: "#FF9A00" },
                    ],
                    category: "design",
                    image: base + "image/the_blue_inside_you.png",
                    pdf: base + "image/the_blue_inside_you.pdf",
                },
                {
                    title: "SUBWAY",
                    description: "브랜드의 신선함을 시각적으로 표현한 광고 영상",
                    type: "일러스트 및 일부 영상 제작 참여",
                    tools: [
                        { name: "Illustrator", color: "#FF9A00" },
                        { name: "After Effects", color: "#9999FF" },
                        { name: "HTML", color: "#E34F26" },
                        { name: "CSS", color: "#1572B6" },
                    ],
                    category: "video",
                    image: base + "image/subway.png",
                    github: "https://yeon-11.github.io/subway-advertising/",
                },
                {
                    title: "식품안전나라",
                    description: "식품안전정보원 공모전에 출품한 공식 홍보 영상",
                    type: "일러스트 및 일부 영상 제작 참여",
                    tools: [
                        { name: "Illustrator", color: "#FF9A00" },
                        { name: "After Effects", color: "#9999FF" },
                    ],
                    category: "video",
                    image: base + "image/video_thumb1.png",
                    video: base + "video/dream_promo1.mp4",
                },
                {
                    title: "키네틱 타이포그래피",
                    description: "가사의 흐름을 시각화한 키네틱 타이포 모션 영상",
                    type: "일부 가사 구간 제작 참여",
                    tools: [
                        { name: "After Effects", color: "#9999FF" },
                    ],
                    category: "video",
                    image: base + "image/video_thumb2.png",
                    video: base + "video/dream_promo2.mp4",
                },
                {
                    title: "addct",
                    description: "기존 홈페이지를 나만의 스타일로 리디자인",
                    type: "기획·디자인·제작",
                    tools: [
                        { name: "HTML", color: "#E34F26" },
                        { name: "CSS", color: "#1572B6" },
                        { name: "Bootstrap", color: "#7952B3" },
                    ],
                    category: "web",
                    image: base + "image/addct.png",
                    github: "https://yeon-11.github.io/addct-redesign/",
                },
                {
                    title: "Antenna",
                    description: "음악 레이블의 정체성을 시각적으로 재해석한 페이지",
                    type: "특정 페이지 제작 참여",
                    tools: [
                        { name: "HTML", color: "#E34F26" },
                        { name: "CSS", color: "#1572B6" },
                        { name: "SCSS", color: "#CD6799" },
                    ],
                    category: "web",
                    image: base + "image/antenna.png",
                    github: "https://yeon-11.github.io/antenna-redesign/",
                },
                {
                    title: "미드림성형외과",
                    description: "의료기관 홈페이지를 현대적 스타일로 리디자인",
                    type: "특정 페이지 제작 참여",
                    tools: [
                        { name: "Vue", color: "#42B883" },
                        { name: "CSS", color: "#1572B6" },
                        { name: "SCSS", color: "#CD6799" },
                        { name: "Figma", color: "#A259FF" },
                    ],
                    category: "web",
                    image: base + "image/meedream.png",
                    github: "https://yeon-11.github.io/meedream-redesign/",
                },
                // {
                //     title: "React 미니 블로그",
                //     description: "글 작성, 수정, 삭제가 가능한 블로그 웹앱 프로토타입",
                //     tools: [
                //         { name: "HTML", color: "#E34F26" },
                //         { name: "CSS", color: "#1572B6" },
                //         { name: "React", color: "#61DAFB" },
                //     ],
                //     category: "web",
                //     image: "https://via.placeholder.com/800x600?text=React+Blog",
                //     github: "https://yeon-11.github.io/",
                // },
                // {
                //     title: "Python 데이터 시각화",
                //     description: "Python으로 데이터를 시각화하고 Matplotlib으로 그래프 구현",
                //     tools: [
                //         { name: "Python", color: "#3776AB" },
                //     ],
                //     category: "web",
                //     image: "https://via.placeholder.com/800x600?text=Python+Visualization",
                //     github: "https://yeon-11.github.io/",
                // },
            ],
        }
    },

    computed: {
        // 선택된 카테고리만 필터링
        filteredProjects() {
            if (this.selectedCategory === "all") {
                return this.projects;
            }
            return this.projects.filter(p => p.category === this.selectedCategory);
        },
        // 디바이스 크기에 따라 페이지당 몇 개 보여줄지 계산
        projectsPerPage() {
            const width = window.innerWidth;
            if (width <= 600) return 2;
            if (width <= 960) return 6;
            return 6;
        },
        // 전체 페이지 수 계산
        pageCount() {
            return Math.ceil(this.filteredProjects.length / this.projectsPerPage);
        },
        // 현재 페이지에 보여줄 프로젝트만 반환
        paginatedProjects() {
            const start = (this.currentPage - 1) * this.projectsPerPage;
            return this.filteredProjects.slice(start, start + this.projectsPerPage);
        },
    },
    methods: {
        // 영상 모달 열기
        openVideoModal(project) {
            this.selectedVideo = project.video || project.youtube;
            this.selectedTitle = project.title;
            this.videoDialog = true;
        },
        // 화면 크기 변화 시 현재 페이지 리셋
        handleResize() {
            const newPerPage = this.projectsPerPage;
            const maxPage = Math.ceil(this.filteredProjects.length / newPerPage);
            if (this.currentPage > maxPage) {
                this.currentPage = maxPage;
            }
        },
        mounted() {
            // 페이지 로드시 리사이즈 이벤트 등록
            window.addEventListener("resize", this.handleResize);
            this.handleResize(); // 디바이스 크기에 맞는 조정
        },
        beforeUnmount() {
            // 컴포넌트 해제 시 이벤트 제거
            window.removeEventListener("resize", this.handleResize);
        }
    }
};
</script>

<style scoped>
/* 섹션 타이틀 - SUITE-Bold 적용 */
h2.text-h4 {
    font-family: 'SUITE-Bold', sans-serif;
    font-weight: 700;
}

/* 카드 높이 균일화 및 내부 정렬 */
.equal-height {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
}

/* 카테고리 토글 버튼 hover 시 색상 변경 */
.v-btn-toggle .v-btn:hover {
    background-color: #4F5D75 !important;
    color: white !important;
}
</style>
