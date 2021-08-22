<template>
  <Layout>
    <div class="journal">
    	<div class="container journal-container">
    		<div class="journal-header">
    			<h1 class="journal-title">{{ journal.title }}</h1>
    			<div class="journal-meta">
    				<div class="journal-author">
    					<span class="label">Author</span>
    					<span class="author-name">{{ journal.author }}</span>
    				</div>
    				<div class="journal-date">
    					<span class="label">Date</span>
    					<div>{{ getDate(journal.published_at) }}</div>
    				</div>
    				<div class="journal-time">
    					<span class="label">Time</span>
    					<span>{{ journal.time }}</span>
    				</div>
    			</div>
    		</div>
    		<div class="journal-content" v-html="mdToHtml(journal.content)"></div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query ($id: ID!){
  strapiJournal(id: $id) {
    id,
    title,
    author,
    published_at,
    content,
    time
  }
}
</page-query>

<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt()

const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']

export default {
  name: 'JournalDetailPage',
  computed: {
    journal() {
      return this.$page.strapiJournal
    }
  },
  methods: {
    mdToHtml(markdown) {
      return md.render(markdown)
    },
    getDate(date) {
      const d = new Date(date)
      return `${d.getDate()}. ${months[d.getUTCMonth()]} ${d.getFullYear()}`
    }
  }
}
</script>

<style scoped>
.journal-container {
  max-width: 840px;
}
.journal-header {
  padding: 2rem 0 4rem;
}
.journal-title {
  font-size: 4rem;
  margin: 0 0 4rem;
  padding: 0;
}
.journal-meta {
  display: flex;
  flex-wrap: wrap;
  font-size: .8rem;
}
.journal-meta > div {
  margin-right: 4rem;
}
.journal-meta > div:last-of-type {
  margin: 0;
}
</style>
