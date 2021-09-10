<template>
  <div class="app">
    <aside>
      <div class="sidebar">
        <form @submit.prevent="onSubmit">
          <input v-model.trim="form.title" placeholder="Title" type="text">
          <input v-model="form.date" placeholder="Date" type="date">
          <textarea v-model.trim="form.text" placeholder="Text" type="text"></textarea>
          <button type="submit">Add</button>
        </form>

        <ul class="items-list">
          <li v-for="item in items" :key="item.id">
            <div class="list-item">
              <span>{{ item.title }}</span>
              <span @click="removeItem(item.id)">X</span>
            </div>
          </li>
        </ul>
      </div>
    </aside>
    <main>
      <div class="container">
        <div class="row">
          <div class="large" ref="largeRef">
            <ContentHighlights
                :available-space="availableSpaceLarge"
                :items="items"
                :backgroundImage="backgroundImage"
                :category="category"
                :itemBackgroundColor="itemBackgroundColor"
            />
          </div>
        </div>
        <div class="row">
          <div class="medium" ref="mediumRef"
               v-for="i in 2"
               :key="i">
            <ContentHighlights
                :available-space="availableSpaceMedium"
                :items="items"
                :backgroundImage="backgroundImage"
                :category="category"
                :itemBackgroundColor="itemBackgroundColor"
            />
          </div>
        </div>
        <div class="row">
          <div class="small" ref="smallRef"
               v-for="i in 3"
               :key="i">
            <ContentHighlights
                :available-space="availableSpaceSmall"
                :items="items"
                :backgroundImage="backgroundImage"
                :itemBackgroundColor="itemBackgroundColor"
                :category="category"
            />
          </div>
        </div>

      </div>
    </main>

  </div>

</template>

<script>
import ContentHighlights from "@/components/ContentHighlights.vue";
import feedIcon from "@/assets/feed-icon.svg";
export default {
  name: "App",
  components: { ContentHighlights },
  data() {
    return {
      form: {
        title: 'test 3',
        date: new Date().toISOString().slice(0, 10),
        text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aut deleniti deserunt eius eum explicabo fugiat maiores quaerat recusandae ullam voluptatum.'
      },
      availableSpaceLarge: 0,
      availableSpaceMedium: 0,
      availableSpaceSmall: 0,
      items: [
        {
          id: 321111323,
          title: `Test article 1`,
          link: 'https://google.com',
          date: '08/20/2021',
          text: 'Lorem ipsum, dolor sit amet consectetur consectetur consectetur adipisicing elit. Eos quam sint rem doloremque dignissimos eum aliquid. Totam, tenetur minima.',
        },
        {
          id: 3235454323,
          title: `Test article 1`,
          link: 'https://google.com',
          date: '08/20/2021',
          text: 'Lorem ipsum, dolor icing elit. Eos quam sint rem doloremque dignissimos eum aliquid. Totam, tenetur minima.',
        },
        {
          id: 32666323,
          title: `Test article 1`,
          link: 'https://google.com',
          date: '08/20/2021',
          text: 'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos quam si dignissimos  consectetureum aliquid. Tot consecteturam, tenetur minima.',
        },
      ],
      backgroundImage: 'https://thumbs.dreamstime.com/b/shopping-supermarket-shopping-cart-view-motion-blur-68328476.jpg',
      itemBackgroundColor: '#fff',
      category: {
        label: 'Featured blogs',
        link: 'https://{{SOME_DOMAIN}}/featured-blogs',
        icon: feedIcon,
      },

    }
  },
  mounted() {
    this.availableSpaceLarge = this.$refs.largeRef.clientWidth
    this.availableSpaceMedium = this.$refs.mediumRef.clientWidth
    this.availableSpaceSmall = this.$refs.smallRef.clientWidth
  },
  methods: {
    onSubmit() {
      if (!this.form.title && !this.form.date && !this.form.text) {
        return false
      }
      if (this.items.length === 4) {
        return  false
      }

      this.items.push({
        id: Math.floor(Math.random() * 10),
        ...this.form
      })
    },
    removeItem(id) {
      this.items = this.items.filter(i => i.id !== id)
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap');
*{
  margin: 0;
  padding: 0;
}

body {
  font: 16px 'Open Sans', sans-serif;
  line-height: 1.6;
  box-sizing: border-box;
}

.app{
  display: flex;
  padding: 2rem;
}

aside {
  flex-basis: 33%;
  position: relative;
}
.sidebar {
  position: fixed;
  width: 30%;
  background-color: #ccc;
}
main {
  flex-basis: 67%;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.row {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 20px;
}

.large {
  flex-basis: 100%;
  margin-bottom: 20px;
}
.medium {
  flex-basis: 49%;
  margin-bottom: 20px;
}

.small{
  flex-basis: 32%;
  margin-bottom: 20px;
}

form {
  padding: 15px;
}

input, textarea {
 display: block;
  width: 100%;
  height: 40px;
  margin-bottom: 10px;
}

textarea {
  height: 80px;
}

.items-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  padding: 10px;
}
.list-item{
  display: flex;
  justify-content: space-between;
}
</style>
