<template>
  <Layout>
    <div class="books">
      <div class="book" v-for="book in $page.allBookEntry.edges" :key="book.node.id">
        <h4>
          <g-link :to="`showcase/${book.node.id}`">{{ book.node.title }}</g-link>
        </h4>

        <div class="content">
          <div class="img-wrapper">
            <g-image  :src="book.node.cover.medium" />
          </div>

          <div>{{ shortenText(book.node.by_statement) }}</div>
        </div>

        <div class="book-footer">
          <div>{{ book.node.publish_date }}</div>
          <div>By <span v-html="book.node.authors[0].name" /></div>
        </div>
      </div>
    </div>
  </Layout>
</template>

<page-query>
query {
  allBookEntry {
    edges {
      node{
        id
        title
        authors {
          name
        },
        cover {
          medium
        }
        by_statement
        publish_date
      }
    }
  }
}
</page-query>

<script>
export default {
  metaInfo: {
    title: 'Showcase'
  },
  methods: {
    shortenText(text) {
      return text.slice(0,300) + '...'
    }
  }
}
</script>

<style lang="scss" scoped>
.books {
  display: grid;
  grid-gap: 1rem;
  grid-template-columns: repeat(3, 1fr);
  padding: 1rem;
}
.book {
  border-radius: 5px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.26);
  padding: 0 15px 20px;
  background: white;
}

.book a {
  color: teal;
  text-decoration: none;

  &:hover {
    color: darken(teal, 10%);
  }
}

.img-wrapper {
  width: 100%;
  text-align: center;
}
.img-wrapper img {
  height: 200px;
}
.book-footer {
  margin-top: 30px;
  display: flex;
  justify-content: space-between;
}
</style>
