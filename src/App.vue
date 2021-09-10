<template>
  <div class="container">
    <div class="row">
      <div class="large" ref="largeRef">
        <ContentHighlights
            :available-space="availableSpace"
            :items="items"
            :backgroundImage="backgroundImage"
            :num-of-items="numOfItems"
            :category="category"
            :itemBackgroundColor="itemBackgroundColor"
        />
      </div>
    </div>
    <div class="row">
      <div class="medium" ref="mediumRef">
        <ContentHighlights
            :available-space="availableSpaceSmall"
            :items="items"
            :backgroundImage="backgroundImage"
            :num-of-items="numOfItems"
            :category="category"
            :itemBackgroundColor="itemBackgroundColor"
        />
      </div>
      <div class="medium" ref="mediumRef">
        <ContentHighlights
            :available-space="availableSpaceSmall"
            :items="items"
            :backgroundImage="backgroundImage"
            :num-of-items="numOfItems"
            :itemBackgroundColor="itemBackgroundColor"
            :category="category"
        />
      </div>
    </div>
    <div class="row">
        <div class="small" ref="xSmallRef">
          <ContentHighlights
              :available-space="availableSpaceXSmall"
              :items="items"
              :backgroundImage="backgroundImage"
              :num-of-items="numOfItems"
              :itemBackgroundColor="itemBackgroundColor"
              :category="category"
          />
        </div>
      <div class="small" ref="xSmallRef">
        <ContentHighlights
            :available-space="availableSpaceXSmall"
            :items="items"
            :backgroundImage="backgroundImage"
            :num-of-items="numOfItems"
            :itemBackgroundColor="itemBackgroundColor"
            :category="category"
        />
      </div>
      <div class="small" ref="xSmallRef">
        <ContentHighlights
            :available-space="availableSpaceXSmall"
            :items="items"
            :backgroundImage="backgroundImage"
            :num-of-items="numOfItems"
            :itemBackgroundColor="itemBackgroundColor"
            :category="category"
        />
      </div>
    </div>

  </div>
</template>

<script>
import ContentHighlights from "@/components/ContentHighlights.vue";
import feedIcon from "@/assets/feed-icon.svg";
export default {
  name: "App",
  components: {
    ContentHighlights,
  },
  data() {
    return {
      numOfItems: 4,
      availableSpace: 0,
      availableSpaceSmall: 0,
      availableSpaceXSmall: 0,
      items: [
        {
          title: "Test article 1",
          link: "https://google.com",
          date: "AUG 20",
          text:
              "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos quam sint rem doloremque dignissimos eum aliquid. Totam, tenetur minima.",
        },
        {
          title: "Test article 2",
          link: "https://google.com",
          date: "AUG 31",
          text:
              "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos quam sint rem doloremque dignissimos eum aliquid. Totam, tenetur minima.",
        },
        {
          title: "Test article 3",
          link: "https://google.com",
          date: "SEPT 2",
          text:
              "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eos quam sint rem doloremque adipisicing dignissimos eum aliquid. Totam,  adipisicing tenetur minima.",
        },
        {
          title: "Test article 4",
          link: "https://google.com",
          date: "AUG 29",
          text:
              "Lorem ipsum, dolor sit amet consectetur adipisicing  elit. Eos quam sint rem adipisicing doloremque dignissimos eum aliquid. Totam, tenetur adipisicing minima.",
        },
      ],
      backgroundImage: 'https://thumbs.dreamstime.com/b/shopping-supermarket-shopping-cart-view-motion-blur-68328476.jpg',
      itemBackgroundColor: '#fff',
      category: {
        label: "Featured blogs",
        link: "https://{{SOME_DOMAIN}}/featured-blogs",
        icon: feedIcon,
      },

    }
  },
  mounted() {
    this.availableSpace = this.$refs.largeRef.clientWidth
    this.availableSpaceSmall = this.$refs.mediumRef.clientWidth
    this.availableSpaceXSmall = this.$refs.xSmallRef.clientWidth
  },
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
</style>
