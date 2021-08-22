<template>
  <Layout>
    <div class="project">
    	<div class="container">
    		<div class="project-header">
    			<h1 class="project-title">{{ project.name }}</h1>
    			<div class="project-info">
    				<div class="categories-container">
    					<div class="categories">
    						<span class="label">Categories</span>
								<template v-for="category in project.categories">
									<span class="category" :key="category.id">{{ category.name }}</span>
								</template>
    					</div>
    				</div>
    				<div class="year-container">
    					<span class="label">Year</span>
    					<div>{{ getYear(project.published_at) }}</div>
    				</div>
    			</div>
    		</div>
    		<div class="content">
					<p v-html="mdToHtml(project.content)"></p>
					<p>
						<img 
						  class="g-image g-image--lazy g-image--loading"
							width="2560"
							data-sizes="(max-width: 2560px) 100vw, 2560px"
							:src="`http://106.75.141.156:1337${project.image.url}`">
					</p>
				</div>
    	</div>
    </div>
  </Layout>
</template>

<page-query>
query ($id: ID!) {
  strapiProject(id: $id) {
    id,
    name,
    published_at,
    content,
    image {
      id,
      url
    }
    categories {
      id,
      name
    }    
  }
}
</page-query>

<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt()

export default {
  name: 'ProjectPage',
	computed: {
		project() {
			return this.$page.strapiProject
		}
	},
	methods: {
		getYear(date) {
			return new Date(date).getFullYear()
		},
		mdToHtml(markdown) {
			return md.render(markdown)
		}
	}
}
</script>

<style scoped>
.project-header {
  padding: 10vh 0 4rem;
}
.project-title {
  font-size: 4rem;
  margin: 0 0 4rem;
  padding: 0;
}
.project-info {
  display: flex;
  flex-wrap: wrap;
  font-size: .8rem;
}
.project-info > div {
  margin-right: 4rem;
}
.project-info > div:last-of-type {
  margin: 0;
}

.category:after {
  content: ", ";
}
.category:last-of-type:after {
  content: "";
}
</style>