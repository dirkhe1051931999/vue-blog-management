<template>
  <div class="vb-markdown">
    <div class="vb-markdown-edit">
      <textarea class="markdown-content" v-model="markdownContent"></textarea>
    </div>
    <div class="vb-markdown-html markdown-body" v-html="markdownHtml"></div>
  </div>
</template>

<script>
import marked from "marked";
export default {
  props: {
    content: {
      type: String,
      default: ""
    }
  },
  components: {},
  name: "",
  data() {
    return {
      markdownContent: "",
      markdownHtml: ""
    };
  },
  watch: {
    content() {
      this.markdownContent = this.content;
    },
    markdownContent() {
      this.markdownHtml = marked(this.markdownContent, { sanitize: true });
      this.$emit("syncContent", this.markdownContent);
    }
  },
  methods: {},
  created() {},
  mounted() {
    this.markdownContent = this.content;
  }
};
</script>

<style lang="scss" scope>
.vb-markdown {
  position: relative;
  width: 100%;
  height: auto;
  border: 1px solid #eeeeee;
  .vb-markdown-edit {
    width: 50%;
    height: 100%;
    textarea.markdown-content {
      display: inline-block;
      padding: 0.8em 1.2em;
      width: 100%;
      min-height: 30em;
      max-width: 100%;
      line-height: 1.6;
      border: none;
      outline: none;
      box-sizing: border-box;
    }
  }
  .vb-markdown-html {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    width: 50%;
    padding: 0.8em 1.2em;
    overflow: auto;
    border-left: 1px solid #eeeeee;
    box-sizing: border-box;
    background-color: #f5f5f5;
  }
}
</style>