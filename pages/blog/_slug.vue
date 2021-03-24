<template>
  <v-container class="slug">
    <h1 class="slug_title">
      {{ article.fields.title }}
    </h1>
    <p class="slug_date">{{ article.sys.updatedAt }}</p>



<div class="blog-content" v-html="$md.render(article.fields.body)"></div>

  <!--  <div v-html="mkbody" />
<div v-html="this.kaigyo"></div>
     <p> {{ article.fields.body.content[0].content[0].value }}</p>

  -->
    </div>
  </v-container>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
import marked from 'marked';
import hljs from 'highlight.js';
const client = createClient()
export default {
  props: {
    id: {
      type: String,
      default: ''
    }
  },
  computed: {
    kaigyo() {
      let str = new String(this.article.body);//.replace(/\<br\>/g, "");
      return str; 
    },
    mkbody() {
      return marked(this.post.fields.body);
    }
  },
  created() {
    marked.setOptions({
      langPrefix: '',
      highlight: function(code, lang) {
        return hljs.highlightAuto(code, [lang]).value
      }
    })
  },
  transition: 'slide-right',
  async asyncData({ env, params }) {
    return await client
      .getEntry(params.sys)
      .then(entrie => {
        return {
          article: entrie
        }
      })
      .catch(console.error)
  }
}
</script>