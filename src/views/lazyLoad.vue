<template>
    <div class="container" ref="container">
        <ul class="list" ref="list">
            <img class="item img-box" v-for="i in 100" :key="i" ref="item" :id="`id_${i}`" :data-src="image" data-alt="节约用水"/>
        </ul>
    </div>
</template>

<script>
  import img from "../assets/saveWater.jpg";

  export default {
    name: "lazyLoad",
    data() {
      return {
        image: img
      };
    },
    methods: {
      initInterSectionObserver() {
        try {
          new IntersectionObserver(entries => {
            entries.map(item => {
              console.log(item);
            });
          });
        } catch (e) {
          console.log(e);
        }
      }
    },
    mounted() {
      /*
      * new IntersectionObserver(callback,options)
      * @param callback 接收参数 entries [Array]
      *    @param  boundingClientRect:空间信息
      *    @param  intersectionRatio:元素可见区域的占比
      *    @param  isIntersecting:判断元素是否可见
      *    @param  target:目标节点，就跟event.target一样
      * @options {root,rootMargin}
      *    @root  指定父元素，默认为视窗
      *    @rootMargin   触发交叉的偏移值，默认为"0px 0px 0px 0px"（上左下右，正数为向外扩散，负数则向内收缩）
      *
      * 常用方法
      *
      *  function  observe  开始监听一个目标元素 @param 节点
      *  function  unobserve   停止监听一个目标元素
      *  function  takeRecords  返回所有监听的目标元素集合
      *  function
      *
      * */


      let observer = new IntersectionObserver(entries => {
        entries.forEach(item => {

          if (item.isIntersecting) {
            item.target.classList.add("join");
            item.target.src = item.target.dataset.src;
            item.target.alt = item.target.dataset.alt;
          } else {
            item.target.classList.remove("join");
            item.target.src = "";
            item.target.alt = "";
          }
        });
      }, {
        root: document.querySelector("body"),
        rootMargin: "0px 0px 240px 0px"
      });
      this.$refs.item.map(item => {
        observer.observe(item);
      });
    }
  };
</script>

<style scoped lang="scss">
    .container {
        .list {
            .item {
                position: relative;
                display: block;
                width: 300px;
                height: 200px;
                &.join {
                    animation: join .1s ease-in;
                }
                &.out {
                    animation: out .1s ease-out;
                }
            }
        }
    }

    @keyframes join {
        0% {
            opacity: 0;
        }
        100% {
            opacity: 1;
            transform: translate(0, 0);
        }
    }

    @keyframes out {
        0% {
            opacity: 1;

        }
        100% {
            opacity: 0;
            transform: translate(-20px, -20px);
        }
    }
</style>
