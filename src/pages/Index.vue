<template>
  <Layout>
    <div class="container">
      <div class="hero">
  			<h1 class="hero-title">{{ hero.title }}</h1>
  			<h2 class="hero-subtitle">
  			  {{ hero.subtitle }}
  			</h2>
  		</div>

			<div class="projects">
				<div 
				  class="project"
					v-for="project in projects" 
				  :key="project.id">
					<g-link class="project-link" :to="`/projects/${project.id}`">
						<img 
						  class="thumbnail g-image g-image--lazy g-image--loaded"
							width="2560"
							data-sizes="(max-width: 2560px) 100vw, 2560px"
							:src="'http://106.75.141.156:1337' + project.image.url"
							:alt="project.name">
						<h3 class="project-title">{{ project.name }}</h3>
						<div class="categories">
							<span 
							  class="category"
								v-for="category in project.categories"
								:key="category.id">{{ category.name }}</span>
						</div>
					</g-link>
				</div>
			</div>
    </div>

    <div>
  		<div class="latest-journals-heading container">
  			<span class="label">Latest and greatest</span>
  		</div>
  		<div class="latest-journals">
  			<div class="container">
  				<g-link 
					  class="journal"
						v-for="journal in journals"
						:key="journal.id"
					  :to="`/journal/${journal.id}`">
  					<h3 class="journal-title">{{ journal.title }}</h3>
  				</g-link>
  			</div>
  		</div>
  	</div>
  </Layout>
</template>

<page-query>
query {
  allStrapiHero {
    edges {
      node {
        title,
        subtitle
      }
    }
  }
	allStrapiProject {
    edges {
      node {
				id,
        name,
        image {
					id,
          url
        },
        categories {
					id,
          name
        }
      }
    }
  }
	allStrapiJournal {
    edges {
      node {
        id,
        title
      }
    }
  }
}
</page-query>

<script>
export default {
  name: 'HomePage',
  metaInfo: {
    title: 'Portfolio'
  },
	computed: {
		hero() {
			return this.$page.allStrapiHero.edges[0].node
		},
		projects() {
			return this.$page.allStrapiProject.edges.map(item => item.node)
		},
		journals() {
			return this.$page.allStrapiJournal.edges.map(item => item.node)
		}
	}
}
</script>

<style scoped>
.projects {
	display: grid;
	grid-template-columns: 1fr 1fr;
	grid-gap: 4rem;
}
.project {
	grid-column: auto/span 1;
	text-align: center;
}
.project-link {
  text-decoration: none;
}
.project-title {
	font-size: 1rem;
	color: var(--color-contrast);
	margin: 2rem 0 1rem;
}

.categories {
	font-size: .8rem;
	color: var(--color-contrast-1);
}
.category {
	margin-right: .8rem;
}
.category:last-of-type {
	margin: 0;
}
.project:hover .thumbnail {
	transform: scale(1.02);
	box-shadow: 0 20px 40px -20px rgba(0, 0, 0, .25);
}
.thumbnail {
	height: 560px;
	-o-object-fit: cover;
	object-fit: cover;
	transition: all .15s ease;
	box-shadow: 0 0 40px -20px rgba(0, 0, 0, .25);
}

@media (min-width: 920px) {
	.project {
		grid-column: auto/span 1;
	}

	.project:nth-child(3n + 1) {
		grid-column: auto/span 2;
	}
}

.latest-journals-heading {
	margin-top: 6rem;
	margin-bottom: 1rem;
	font-size: .6rem;
	font-weight: 400;
	text-transform: uppercase;
}
.latest-journals {
	max-width: 100%;
	margin: 0 2rem;
	border: 1px solid var(--color-base-1);
}
.latest-journals > .container {
	display: flex;
	flex-wrap: wrap;
}
.journal {
	flex: 0 0 100%;
	display: block;
	padding: 2rem;
	transition: background .25s ease;
	text-decoration: none;
	border-bottom: 1px solid var(--color-base-1);
}
.journal:last-of-type {
	border-bottom: 0;
}
.journal:hover {
	background: var(--color-base-1);
}
.journal-title {
	font-size: 1rem;
	line-height: 1.35;
}

@media (min-width: 580px) {
	.journal {
		flex: 0 0 50%;
	}
	.journal:first-child {
		border-right: 1px solid var(--color-base-1);
	}
	.journal:first-child, .journal:nth-child(2) {
		border-bottom: 1px solid var(--color-base-1);
	}
	.journal:nth-child(3) {
		border-right: 1px solid var(--color-base-1);
		border-bottom: 0;
	}
}

@media (min-width: 920px) {
	.journal {
		flex: 0 0 25%;
	}
	.journal:first-child,
	.journal:nth-child(2),
	.journal:nth-child(3) {
		border: 0;
		border-right: 1px solid var(--color-base-1);
	}
	.latest-journals {
		margin: 0;
		border-left: 0;
		border-right: 0;
		border-top: 1px solid var(--color-base-1);
		border-bottom: 1px solid var(--color-base-1);
	}
}
</style>
