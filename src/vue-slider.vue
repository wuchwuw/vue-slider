<template>
  <div id="slider">
    <div id="slider-wrap">
      <div class="slider-item" v-for="item in images" :key="item">
        <img class="slider-img" :src="item" alt="">
      </div>
    </div>
  </div>
</template>

<script>

const shared = {
  width: window.innerWidth
}

export default {
  name: 'VueSlider',
  data () {
    return {
      images: [
        'http://y.gtimg.cn/music/common/upload/MUSIC_FOCUS/1205042.jpg',
        'http://y.gtimg.cn/music/common/upload/MUSIC_FOCUS/1203123.jpg',
        'http://y.gtimg.cn/music/common/upload/MUSIC_FOCUS/1204325.jpg',
        'http://y.gtimg.cn/music/common/upload/MUSIC_FOCUS/1202412.jpg',
        'http://y.gtimg.cn/music/common/upload/MUSIC_FOCUS/1203899.jpg'
      ],
      currentIndex: shared.width
    }
  },
  mounted () {
    this.initSlider()
  },
  methods: {
    initSlider () {
      const length = this.images.length + 2
      let wrap = document.getElementById('slider-wrap')
      let items = document.getElementsByClassName('slider-item')
      this.handleLoop(wrap, items)
      wrap.style.width = `${shared.width * length}px`
      for (let i = 0; i < items.length; i++) {
        items[i].style.width = `${shared.width}px`
      }
      this.transitionWrap(wrap)
    },
    transitionWrap (wrap) {
      wrap.style.transform = `translate3d(${-this.currentIndex}px, 0px, 0px)`
      setInterval(() => {
        this.next(wrap)
      }, 2000)
    },
    handleLoop (wrap, items) {
      let firstChild = items[0].cloneNode(true)
      let lastChild = items[items.length - 1].cloneNode(true)
      wrap.insertBefore(lastChild, items[0])
      wrap.appendChild(firstChild)
      wrap.addEventListener('transitionend', () => {
        if (this.currentIndex === shared.width * 6) {
          this.currentIndex = shared.width
          wrap.style.transitionDuration = '0ms'
          wrap.style.transform = `translate3d(${-this.currentIndex}px, 0px, 0px)`
        }
      })
    },
    next (wrap) {
      // 375 750 1225 1500 1875 2250
      this.currentIndex += shared.width
      wrap.style.transitionDuration = '300ms'
      wrap.style.transform = `translate3d(${-this.currentIndex}px, 0px, 0px)`
    },
    prev () {

    }
  }
}
</script>


<style>
  #slider {
    width: 100%;
    font-size: 0;
    overflow: hidden;
  }
  #slider-wrap {
    position: relative;
    overflow: hidden;
  }
  .slider-item {
    float: left;
  }
  .slider-img {
    width: 100%;
    -webkit-backface-visibility: hidden
  }
</style>
