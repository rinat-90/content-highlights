<template>
  <section :style="cssVars">
    <div class="wrapper">
      <h2 class="heading">{{ category.label }}</h2>
      <div class="banner">
        <div class="banner-list">
          <div class="banner-list-item__wrapper" ref="bannerRef">
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
              <p>
                <span>{{ item.text }}</span>
              </p>
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
  data(){
    return {
      height: 0
    }
  },
  computed: {
    isOdd(){
      return this.items.length % 2 !== 0
    },
    maxHeight(){
      return this.height > 0 ? { 'height': this.height + 'px'} : {'height': 'auto' }
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
        '--item-height': this.height > 0 ? this.height + 'px' : 'auto'
      };
    },
  },
  methods: {
    parseDate(str) {
      const date = new Date(str)
      const months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
      return `${months[date.getMonth()]} ${date.getDate()}`
    },
    getMaxHeight (){
      const elems = this.$refs.bannerRef.children
      if (elems.length) {
        for (let el in elems) {
          if (elems[el].children){
            if (elems[el].lastChild.clientHeight > this.height) {
              this.height = elems[el].lastChild.clientHeight
            }
            if (elems[el].lastChild.clientHeight > elems[el].lastChild.firstChild.offsetHeight) {
              this.height = elems[el].lastChild.firstChild.offsetHeight
            }
            if (elems[el].lastChild.clientHeight < elems[el].lastChild.firstChild.offsetHeight) {
              this.height = elems[el].lastChild.firstChild.offsetHeight
            }
          }
        }
      }

    }
  },
  mounted() {
    this.$nextTick(this.getMaxHeight)
    this.$nextTick(() => {
      window.addEventListener('resize', this.getMaxHeight)
    })
  },
  unmounted() {
    window.removeEventListener('resize', this.getMaxHeight)
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
  padding: 20px;
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
  height: var(--item-height);
}

.banner-list-item__date{
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  content: '';
  width: 35px;
  height: 35px;
  font-size: 12px;
  border-radius: 50%;
  background-color: #000;
  text-align: center;
  padding: 10px;
  color: #fff;
  left: -30px;
  top: -25px;
}

.banner-list-item__date > span{
  font-size: 14px;
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

