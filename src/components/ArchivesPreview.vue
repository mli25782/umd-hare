<template>
  <div id="article">
    <div id="title">
      <arl :article="article">{{ article.title }}</arl>
    </div>
    {{ dateStr }} | {{ article.authorFullName }} | {{ article.categoryLabel }}
    <hr />
  </div>
</template>

<script>
import moment from "moment";
import ArticleLink from "@/components/ArticleLink";
export default {
  name: "ArchivesPreview",
  props: ["article"],
  components: {
    arl: ArticleLink,
  },
  data() {
    return {
      dateStr: "",
    };
  },
  mounted() {
    const dateCreated = moment(this.article.dateCreated);
    const dateVisible = moment(this.article.dateVisible);
    const date = dateCreated.isAfter(dateVisible) ? dateCreated : dateVisible;
    this.dateStr = this.$formatDate(date);
  },
};
</script>

<style scoped>
#article {
  text-align: left;
  font-size: 11pt;
}

#title {
  font-size: 20pt;
}
</style>
