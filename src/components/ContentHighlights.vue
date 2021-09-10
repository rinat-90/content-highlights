<template>
  <section :style="cssVars">
    <div class="wrapper">
      <h2 class="heading">{{ category.label }}</h2>
      <div class="banner">
        <div class="banner-list">
          <div class="banner-list-item__wrapper">
            <a
                v-for="item in items"
                :key="item.id"
                :href="item.link"
                class="banner-list-item"
            >
              <span class="banner-list-item__date">
                <span>{{ parseDate(item.date)}}</span>
              </span>
              <h3>{{ item.title }}</h3>
              <p>{{ item.text }}</p>
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>

export default {
  name: 'ContentHighlights',
  props: {
    availableSpace: Number,
    itemBackgroundColor: String,
    backgroundImage: String,
    category: Object,
    items: Array,
  },
  computed: {
    isOdd(){
      return this.items.length % 2 !== 0
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
    parseDate(str) {
      const date = new Date(str)
      const months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
      return `${months[date.getMonth()]} ${date.getDate()}`
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

.banner-list {
  display: flex;
  justify-content: var(--align-self-item);
  height: 100%;
  min-height: 500px;
  gap: 20px;
}
.banner-list-item__wrapper {
  display: flex;
  flex-basis: var(--item-width);
  align-self: center;
  flex-direction: column;
  padding: 1.5rem;
}



.banner-list-item {
  background-color: var(--item-bg-color);
  padding: 15px;
  margin-bottom: 50px;
  box-shadow: 0px 1px 5px #ddd;
  position: relative;
  z-index: 2;
  text-decoration: none;
}

.banner-list-item:last-child {
  margin-bottom: 0;
}

.banner-list-item h3 {
  text-transform: uppercase;
  font-size: 20px;
  color: #494949;
}

.banner-list-item p {
  color: #494949;
  white-space: break-spaces;
}

.banner-list-item__date{
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  content: '';
  width: 40px;
  height: 40px;
  font-size: 12px;
  border-radius: 50%;
  background-color: #000;
  text-align: center;
  padding: 10px;
  color: #fff;
  left: -35px;
  top: -35px;
}

.banner-list-item__date > span{
  font-size: 16px;
  line-height: 1.2;
  text-transform: uppercase;
  white-space: break-spaces;
}



.heading{
  background-color: #e9eae9;
  text-transform: uppercase;
  padding: 10px 10px 10px 100px;
  margin-bottom: 10px;
  position: relative;
  font-size: 20px;
}

.heading:before{
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




</style>

