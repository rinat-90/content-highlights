<template>
  <section class="wrapper" :style="cssVars" ref="wrapperRef">
    <div>
      <h2 class="section-heading">
        {{ category.label }}
      </h2>
      <div class="banner">
        <div class="banner-items-wrapper">
          <div class="banner-item-wrapper">
            <article
                ref="itemRef"
                @click="onItemClicked(item)"
                v-for="item in items.slice(0, numOfItems)"
                :key="item.title"
                class="banner-item"
            >
              <span class="banner-item-date">
                <span>AUG</span>
                <span>20</span>
              </span>
              <h3>{{ item.title }}</h3>
              <p>{{ item.text }}</p>
            </article>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>

export default {
  name: "ContentHighlights",
  props: {
    numOfItems: Number,
    availableSpace: Number,
    itemBackgroundColor: String,
    backgroundImage: String,
    category: Object,
    items: Array,
  },
  computed: {
    isOdd(){
      return this.numOfItems % 2 !== 0
    },
    cssVars() {
      return {
        "--bg-img": `url(${this.backgroundImage})`,
        "--item-bg-color": `${this.itemBackgroundColor}`,
        "--item-width": this.availableSpace > 760
            ? `${this.availableSpace / 2.5 }px`
            : this.availableSpace > 550
                ? `${this.availableSpace / 1.5 }px`
                : `${this.availableSpace / 1.2 }px`,
        '--align-self-item': this.isOdd ? 'center' : 'end',
        '--heading-icon': `url(${this.category.icon})`,
      };
    },
  },
  methods: {
    onItemClicked(item) {
      console.log(item)
    }
  }
};
</script>

<style scoped>
.wrapper{
  height: 100%;
  min-height: 500px;
}
.banner {
  background: var(--bg-img);
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
  position: relative;
  height: 100%;
  width: 100%;
  padding: 20px 0;
}
.banner::after{
  content: '';
  display: block;
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
  background-color: rgba(0,0,0, 0.2);
}

.banner-items-wrapper {
  display: flex;
  justify-content: var(--align-self-item);
  height: 100%;
  min-height: 500px;
  gap: 20px;
}
.banner-item-wrapper {
  display: flex;
  flex-basis: var(--item-width);
  align-self: center;
  flex-direction: column;
  padding: 1.5rem;
}

.banner-item h3 {
  text-transform: uppercase;
  font-size: 20px;
  color: #494949;
}

.banner-item p {
  color: #494949;
  white-space: break-spaces;
}

.banner-item {
  background-color: var(--item-bg-color);
  padding: 15px;
  margin-bottom: 50px;
  box-shadow: 0px 1px 5px #ddd;
  position: relative;
  z-index: 2;

}

.banner-item-date{
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  content: '';
  width: 50px;
  height: 50px;
  font-size: 12px;
  border-radius: 50%;
  background-color: #000;
  text-align: center;
  color: #fff;
  left: -25px;
  top: -25px;
}

.banner-item:last-child {
  margin-bottom: 0;
}

.section-heading{
  background-color: #ccc;
  text-transform: uppercase;
  padding: 10px 10px 10px 100px;
  margin-bottom: 10px;
  position: relative;
  font-size: 20px;
}

.section-heading:before{
  content: '';
  margin-left: 15px;
  background: var(--heading-icon);
  background-repeat: no-repeat;
  background-position: center center;
  display: block;
  bottom: 5px;
  left: 0;
  position: absolute;
  height: 75px;
  width: 75px;
  border-radius: 50%;
  background-color: #000;
}

.icon{
  width: 50px;
  height: 50px;
}

</style>

