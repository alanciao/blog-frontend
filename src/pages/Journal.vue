<template>
  <Layout>
    <div class="container">
    	<div class="journal-hero">
    		<h1 class="journal-header">
              a wise person once said...
            </h1>
        </div>
    </div>

    <g-link 
      class="journal-post"
      v-for="journal in journals"
      :key="journal.key"
      :to="`/journal/${journal.id}`">
    	<div class="container journal">
    		<h2 class="journal-title">{{ journal.title }}</h2>
        <p class="journal-excerpt">{{ journal.subtitle }}</p>
    	</div>
    </g-link>
  </Layout>
</template>

<page-query>
query {
	allStrapiJournal(
    sortBy: "created_at",
    order: DESC
  ) {
    edges {
      node {
        id,
        title,
        subtitle
      }
    }
  }
}
</page-query>

<script>
export default {
  name: 'JournalPage',
  metaInfo: {
    title: 'Portfolio'
  },
  computed: {
    journals() {
      return this.$page.allStrapiJournal.edges.map(item => item.node)
    }
  }
}
</script>

<style scoped>
.container.journal {
  max-width: 720px;
}
.journal-hero {
  padding: 4rem 0;
  text-align: center;
  color: var(--color-base-1);
}
.journal-header {
  font-size: 3rem;
  font-weight: 700;
  padding: 0;
  margin: 0;
}
.journal-post {
  display: block;
  padding: 2rem 0;
  text-decoration: none;
  transition: background .5s ease;
}
.journal-post > * {
  transition: transform .5s ease;
}
.journal-post:hover {
  background-color: var(--color-base-1);
}
.journal-post:hover > * {
  transform: translateX(4rem);
}
.journal-post h1, .journal-post h2 {
  margin: 0;
  padding: 0;
}
.journal-title {
  font-size: 2rem;
  color: var(--color-contrast);
}
.journal-excerpt {
  color: var(--color-contrast-1);
}

@media (min-width: 560px) {
  .journal-post {
    padding: 3rem 0;
  }
}

@media (min-width: 860px) {
  .journal-post {
    padding: 5rem 0;
  }
}
</style>
