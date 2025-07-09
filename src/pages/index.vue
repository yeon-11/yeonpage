<template>
  <div>
    <!-- 섹션들 -->
    <v-container class="py-10">
      <div id="about">
        <AboutSection />
      </div>
      <div id="skills">
        <SkillSection />
      </div>
      <div id="projects">
        <ProjectSection />
      </div>
      <div id="contact">
        <ContactSection />
      </div>
    </v-container>
  </div>
</template>

<script>
import AboutSection from "@/components/AboutSection.vue";
import SkillSection from "@/components/SkillSection.vue";
import ProjectSection from "@/components/ProjectSection.vue";
import ContactSection from "@/components/ContactSection.vue";

export default {
  components: {
    AboutSection,
    SkillSection,
    ProjectSection,
    ContactSection,
  },
  methods: {
    scrollTo(id) {
      const el = document.getElementById(id);
      if (el) el.scrollIntoView({ behavior: "smooth" });
    },
  },
};
</script>