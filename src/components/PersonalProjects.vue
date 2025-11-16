<template>
    <v-container class="py-10 personal-projects-section">
        <!-- 타이틀 -->
        <h2 class="text-h5 font-weight-bold mb-10">📂 Personal Projects</h2>

        <!-- 카테고리 토글 -->
        <v-chip-group v-model="selectedCategory" class="mb-6 category-chips" mandatory>
            <!-- 각 chip에 활성 여부에 따라 클래스 바인딩 -->
            <v-chip value="all" class="category-chip" :class="{ 'category-chip--active': selectedCategory === 'all' }"
                label>
                전체
            </v-chip>

            <v-chip value="design" class="category-chip"
                :class="{ 'category-chip--active': selectedCategory === 'design' }" label>
                디자인
            </v-chip>

            <v-chip value="video" class="category-chip"
                :class="{ 'category-chip--active': selectedCategory === 'video' }" label>
                영상
            </v-chip>

            <v-chip value="web" class="category-chip" :class="{ 'category-chip--active': selectedCategory === 'web' }"
                label>
                웹개발
            </v-chip>
        </v-chip-group>

        <!-- 프로젝트 카드 리스트 -->
        <v-row dense>
            <v-col v-for="(project, index) in filteredProjects" :key="index" cols="12" sm="6" md="4" lg="3"
                class="mb-3">
                <v-card class="mx-auto equal-height" max-width="500">
                    <!-- 이미지 -->
                    <v-sheet class="pa-3" color="transparent" height="300px">
                        <v-img :src="project.image" height="100%" contain />
                    </v-sheet>

                    <!-- 타이틀 -->
                    <v-card-title class="d-flex flex-column px-4 pt-4">
                        <v-chip v-if="project.type" class="mb-2 align-self-start" label size="small"
                            color="grey lighten-2" text-color="black">
                            {{ project.type }}
                        </v-chip>
                        <b>{{ project.title }}</b>
                    </v-card-title>

                    <!-- 설명 + 툴 -->
                    <v-card-text>
                        {{ project.description }}

                        <div class="mt-2 d-flex flex-wrap">
                            <v-chip v-for="(tool, i) in project.tools" :key="i" class="ma-1" variant="outlined"
                                size="small" :color="tool.color">
                                {{ tool.name }}
                            </v-chip>
                        </div>
                    </v-card-text>

                    <!-- 버튼 -->
                    <v-card-actions>
                        <v-btn v-if="project.github" :href="project.github" target="_blank" text>
                            <b>💻 홈페이지 보기</b>
                        </v-btn>

                        <v-btn v-if="project.pdf" :href="project.pdf" target="_blank" text>
                            <b>📄 문서 보기</b>
                        </v-btn>

                        <v-btn v-if="project.video || project.youtube" @click="openVideoModal(project)" text>
                            <b>🎥 영상 보기</b>
                        </v-btn>
                    </v-card-actions>
                </v-card>
            </v-col>
        </v-row>

        <!-- 영상 모달 -->
        <v-dialog v-model="videoDialog" max-width="800px">
            <v-card>
                <v-card-title class="text-h6 mt-4">
                    🎥 {{ selectedTitle }} - 영상 보기
                </v-card-title>

                <v-card-text>
                    <!-- 로컬 mp4 영상 -->
                    <video v-if="selectedVideo && isLocalVideo(selectedVideo)" :src="selectedVideo" controls autoplay
                        style="width: 100%; height: auto"></video>

                    <!-- 유튜브 영상 -->
                    <iframe v-else-if="selectedVideo" :src="getYoutubeEmbedUrl(selectedVideo)" frameborder="0"
                        allowfullscreen style="width: 100%; height: 450px"></iframe>
                </v-card-text>

                <v-card-actions>
                    <v-spacer />
                    <v-btn text @click="videoDialog = false">닫기</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-container>
</template>

<script>
export default {
    name: "PersonalProjects",

    data() {
        const base = import.meta.env.BASE_URL;

        return {
            // 선택된 프로젝트 카테고리
            selectedCategory: "all",

            // 영상 모달 상태
            videoDialog: false,
            selectedVideo: null,
            selectedTitle: "",

            // 이미지/영상 base 경로
            base,

            // 프로젝트 목록
            projects: [
                {
                    title: "PLANLOG",
                    description: "할 일 관리에 최적화된 UI 디자인",
                    type: "기획 및 UI 디자인 중심 참여",
                    tools: [{ name: "Photoshop", color: "#31A8FF" }],
                    category: "design",
                    image: base + "image/planlog.png",
                    github: "https://yeon-11.github.io/planlog/",
                },
                {
                    title: "그대안의블루",
                    description: "청년 우울증을 주제로 한 카드뉴스 콘텐츠",
                    type: "특정 카드 디자인 참여",
                    tools: [{ name: "Illustrator", color: "#FF9A00" }],
                    category: "design",
                    image: base + "image/the_blue_inside_you.png",
                    pdf: base + "image/the_blue_inside_you.pdf",
                },
                {
                    title: "더글로리 Fanmade MV",
                    description:
                        "고통을 마주한 두 인물이 서로의 구원이 되어가는 여정을 감정선 중심으로 재구성한 뮤직비디오",
                    type: "디자인·전체 영상 컷편집",
                    tools: [{ name: "After Effects", color: "#9999FF" }],
                    category: "video",
                    image: base + "image/theglory.png",
                    youtube: "https://youtu.be/_hN_94FQ_dk",
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
                    category: ["design", "video"],
                    image: base + "image/subway.png",
                    video: base + "video/subway.mp4",
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
                    image: base + "image/food.png",
                    video: base + "video/food.mp4",
                },
                {
                    title: "Attitude - 키네틱 타이포그래피",
                    description: "가사의 흐름을 시각화한 키네틱 타이포 모션 영상",
                    type: "일부 가사 구간 제작 참여",
                    tools: [{ name: "After Effects", color: "#9999FF" }],
                    category: "video",
                    image: base + "image/attitude.png",
                    video: base + "video/attitude.mp4",
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
                {
                    title: "10CM 5.0 떡메모지",
                    description:
                        "공식 일러스트를 굿즈 형태로 변환한 90×90mm 떡메모지 (비상업적·비공식 팬메이드)",
                    type: "굿즈 기획·제작",
                    tools: [{ name: "Illustrator", color: "#FF9A00" }],
                    category: "design",
                    image: base + "image/10cm_memo.png",
                    pdf: base + "image/10cm_memo.pdf",
                },
                {
                    title: "공부 기록 사이트",
                    description: "공부한 내용을 기록하고 웹사이트로 구현한 홈페이지",
                    type: "개인 학습 기록·제작",
                    tools: [
                        { name: "HTML", color: "#E34F26" },
                        { name: "CSS", color: "#1572B6" },
                        { name: "Bootstrap", color: "#7952B3" },
                    ],
                    category: "web",
                    image: base + "image/devsign-notes.png",
                    github: "https://yeon-11.github.io/devsign-notes/",
                },
            ],
        };
    },

    computed: {
        // 카테고리 필터링
        filteredProjects() {
            if (this.selectedCategory === "all") return this.projects;

            return this.projects.filter((project) => {
                if (Array.isArray(project.category)) {
                    return project.category.includes(this.selectedCategory);
                }
                return project.category === this.selectedCategory;
            });
        },
    },

    methods: {
        // 영상 모달 오픈
        openVideoModal(project) {
            this.selectedVideo = project.video || project.youtube;
            this.selectedTitle = project.title;
            this.videoDialog = true;
        },

        // 로컬 mp4 여부 체크
        isLocalVideo(link) {
            return link.endsWith(".mp4");
        },

        // 유튜브 링크를 embed URL로 변환
        getYoutubeEmbedUrl(link) {
            const videoId = link.split("youtu.be/")[1]?.split("?")[0];
            return `https://www.youtube.com/embed/${videoId}?rel=0&modestbranding=1`;
        },
    },
};
</script>

<style scoped>
/* 카드 높이 동일 유지 */
.equal-height {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
}

/* 섹션 타이틀 - SUITE-Bold 적용 */
.personal-projects-section h2 {
    font-family: "SUITE-Bold", sans-serif;
}

/* 섹션 내 텍스트 - SUITE-Regular */
.personal-projects-section p,
.personal-projects-section .v-btn,
.personal-projects-section .v-chip,
.personal-projects-section .v-card-title,
.personal-projects-section .v-card-text,
.personal-projects-section .v-card-actions {
    font-family: "SUITE-Regular", sans-serif;
}

/* 카테고리 chip 그룹 */
.category-chips {
    display: flex;
    gap: 8px;
}

/* 카테고리 chip 기본 */
.category-chip {
    border-radius: 999px;
    background-color: #f5f5f5;
    padding: 6px 16px;
    font-weight: 500;
    text-transform: none;
}

/* 선택된 chip */
.category-chip--active {
    background-color: #4f5d75 !important;
    color: #ffffff !important;
    font-weight: 600;
}
</style>
