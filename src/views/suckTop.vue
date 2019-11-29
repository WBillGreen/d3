<template>
    <div class="container" ref="container">
        <ul class="list" ref="list">
            <div class="header" ref="header"></div>
            <li v-for="item in content">
                <div class="title" ref="type" :data-type="item.type">{{item.name}}</div>
                <ul>
                    <li v-for="child in item.child" class="food-main">
                        <img class="food-img" ref="foodImg" :data-src="child.image" :data-alt="child.intr">
                        <div class="food-context">
                            <p class="food-title">{{child.name}}</p>
                            <p class="food-intr">{{child.intr}}</p>
                            <p>
                                <span class="food-price">￥{{child.price}}-</span>
                            </p>
                            <p>
                                <span class="food-number">{{child.number}}</span>
                            </p>
                        </div>
                    </li>
                </ul>
            </li>
        </ul>
    </div>
</template>

<script>
  export default {
    name: "suckTop",
    data() {
      return {
        content: [
          {
            type: 'hot',
            name: "热门",
            child: [{
              name: "肉松热狗",
              image: require('../assets/images/1.jpg'),
              price: 1000,
              discount: 1500,
              intr: "这是美味的肉松热狗",
              number: 1000,
              sold: 200,
              id: 1
            }, {
              name: "皮豌豆",
              image: require('../assets/images/2.jpg'),
              price: 1000,
              discount: 1500,
              intr: "香脆可口的酸辣豌豆",
              number: 1000,
              sold: 200,
              id: 2
            }, {
              name: "蛊中有肉",
              image: require('../assets/images/3.jpg'),
              price: 1000,
              discount: 1500,
              intr: "美味的煲肉汤",
              number: 1000,
              sold: 200,
              id: 3
            }, {
              name: "可可豆腐",
              image: require('../assets/images/4.jpg'),
              price: 1000,
              discount: 1500,
              intr: "神奇的豆腐甜品",
              number: 1000,
              sold: 200,
              id: 4
            }]
          },
          {
            type: 'free',
            name: "优惠",
            child: [{
              name: "肉松热狗",
              image: require('../assets/images/1.jpg'),
              price: 1000,
              discount: 1500,
              intr: "这是美味的肉松热狗",
              number: 1000,
              sold: 200,
              id: 5
            }, {
              name: "皮豌豆",
              image: require('../assets/images/2.jpg'),
              price: 1000,
              discount: 1500,
              intr: "香脆可口的酸辣豌豆",
              number: 1000,
              sold: 200,
              id: 6
            }, {
              name: "蛊中有肉",
              image: require('../assets/images/3.jpg'),
              price: 1000,
              discount: 1500,
              intr: "美味的煲肉汤",
              number: 1000,
              sold: 200,
              id: 7
            }, {
              name: "可可豆腐",
              image: require('../assets/images/4.jpg'),
              price: 1000,
              discount: 1500,
              intr: "神奇的豆腐甜品",
              number: 1000,
              sold: 200,
              id: 8
            }]
          },
          {
            type: 'dessert',
            name: "甜点",
            child: [{
              name: "肉松热狗",
              image: require('../assets/images/1.jpg'),
              price: 1000,
              discount: 1500,
              intr: "这是美味的肉松热狗",
              number: 1000,
              sold: 200,
              id: 9
            }, {
              name: "皮豌豆",
              image: require('../assets/images/2.jpg'),
              price: 1000,
              discount: 1500,
              intr: "香脆可口的酸辣豌豆",
              number: 1000,
              sold: 200,
              id: 10
            }, {
              name: "蛊中有肉",
              image: require('../assets/images/3.jpg'),
              price: 1000,
              discount: 1500,
              intr: "美味的煲肉汤",
              number: 1000,
              sold: 200,
              id: 11
            }, {
              name: "可可豆腐",
              image: require('../assets/images/4.jpg'),
              price: 1000,
              discount: 1500,
              intr: "神奇的豆腐甜品",
              number: 1000,
              sold: 200,
              id: 12
            }]
          },
          {
            type: 'drinks',
            name: "酒水",
            child: [{
              name: "肉松热狗",
              image: require('../assets/images/1.jpg'),
              price: 1000,
              discount: 1500,
              intr: "这是美味的肉松热狗",
              number: 1000,
              sold: 200,
              id: 13
            }, {
              name: "皮豌豆",
              image: require('../assets/images/2.jpg'),
              price: 1000,
              discount: 1500,
              intr: "香脆可口的酸辣豌豆",
              number: 1000,
              sold: 200,
              id: 14
            }, {
              name: "蛊中有肉",
              image: require('../assets/images/3.jpg'),
              price: 1000,
              discount: 1500,
              intr: "美味的煲肉汤",
              number: 1000,
              sold: 200,
              id: 15
            }, {
              name: "可可豆腐",
              image: require('../assets/images/4.jpg'),
              price: 1000,
              discount: 1500,
              intr: "神奇的豆腐甜品",
              number: 1000,
              sold: 200,
              id: 16
            }]
          }
        ]
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
            item.target.src=item.target.dataset.src;
            item.target.alt=item.target.dataset.alt;
          }else{
            if(item.target.dataset.type){
              console.log(item.target.dataset.type);
            }
          }
          console.log(item.target.dataset.src);
         // this.$refs.header.appendChild(item.target)
        });
      }, {
        root: document.querySelector('body'),
        rootMargin:'0px 0px 240px 0px'
      });
      this.$refs.foodImg.map(item => {
        observer.observe(item);
      });
      this.$refs.type.map(type=>{
        observer.observe(type);
      })
    }
  };
</script>

<style scoped lang="scss">
    .container {
        ul {
           list-style: none;
            padding: 0;
        }
        .title{
            font-size: 14px;
            flood-color: #222222;
            font-weight: bold;
            padding: 10px 20px 10px 10px;
        }
        .food-main{
            box-sizing: border-box;
            padding: 10px;
            display: flex;
            justify-content: space-between;
            .food-img{
                width: 120px;
            }
            .food-context{
                flex: 1;
                box-sizing: border-box;
                padding-left: 20px;
                .food-title{
                    font-size: 14px;
                    color: #222222;
                }
                .food-intr{
                    font-size: 12px;
                    color: #999999;
                }
                .food-price{
                    font-size: 12px;
                    color: #666666;
                }
                .food-number{
                    font-size: 12px;
                    color: #666666;
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
