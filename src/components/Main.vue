<template>
  <div class="schedule">
    <slot name="header">
      <header>{{ title }}</header>
    </slot>
    <main v-if="info.length > 0">
      <section v-for="(item, index) in info" :key="index">
        <div class="title" v-if="show">{{ item.title }}</div>
        <div class="item">
          <div
            v-for="(child, i) in item.list"
            :key="i"
            :style="{
              height:
                index == 0
                  ? configHeight + 'px'
                  : index == info.length - 1
                  ? Math.pow(2, index - 1) * configHeight +
                    (Math.pow(2, index - 1) - 1) * config.mb +
                    'px'
                  : Math.pow(2, index) * configHeight +
                    (Math.pow(2, index) - 1) * config.mb +
                    'px',
              marginBottom: config.mb + 'px',
            }"
          >
            <section
              v-if="index < info.length - 1 && child.length > 0"
              :style="[
                {
                  height:
                    index == 0
                      ? config.initheight + 'px'
                      : index == info.length - 1
                      ? Math.pow(2, index - 2) * configHeight +
                        Math.pow(2, index - 2) * config.mb -
                        config.borderWidth +
                        'px'
                      : Math.pow(2, index - 1) * configHeight +
                        Math.pow(2, index - 1) * config.mb -
                        config.borderWidth +
                        'px',
                },
                {
                  borderWidth: config.borderWidth + 'px',
                  borderColor: config.borderColor,
                  '--height': config.borderWidth + 'px',
                  '--color': config.borderColor,
                },
              ]"
            >
              <div
                :style="[
                  child[0].win ? config.win : config.lose,
                  {
                    top:
                      -(config.itemHeight / 2) - config.borderWidth / 2 + 'px',
                    height: config.itemHeight + 'px',
                    justifyContent: config.justify,
                    borderWidth: config.borderWidth + 'px',
                  },
                ]"
              >
                <span>{{ child[0].name }}</span>
              </div>
              <div
                :style="[
                  child[1].win ? config.win : config.lose,
                  {
                    bottom:
                      -(config.itemHeight / 2) - config.borderWidth / 2 + 'px',
                    height: config.itemHeight + 'px',
                    justifyContent: config.justify,
                    borderWidth: config.borderWidth + 'px',
                  },
                ]"
              >
                <span>{{ child[1].name }}</span>
              </div>
            </section>
            <section
              v-else-if="index == info.length - 1"
              :style="{ height: config.itemHeight + 'px' }"
              class="winBox"
            >
              <div
                class="win"
                :style="[
                  child.win ? config.win : config.lose,
                  {
                    height: config.itemHeight + 'px',
                    justifyContent: config.justify,
                    borderWidth: config.borderWidth + 'px',
                  },
                ]"
              >
                <span>{{ child.name }}</span>
              </div>
            </section>
          </div>
        </div>
      </section>
    </main>
    <slot name="none" v-else>
      <main class="none">暂无数据</main>
    </slot>
  </div>
</template>
<script>
export default {
  name: "Main",
  data() {
    return {
      blue: "blue",
    };
  },
  props: {
    show: {
      type: Boolean,
      default: true,
    },
    info: {
      type: Array,
      default: () => [],
    },
    title: {
      type: String,
      default: "赛程图",
    },
    config: {
      type: Object,
      default: () => {
        return {
          initheight: 50, // 对垒单元格高度
          itemHeight: 40, // 单元格高度
          mb: 10, // 相邻对垒单元格距离
          justify: "flex-start", //文本对其 center flex-end flex-start
          borderWidth: 2, // border宽度
          borderColor: "#f05b5b", // 连接线颜色
          win: {
            // 胜利单元格样式
            backgroundColor: "rgb(250, 224, 224)",
            color: "#f05b5b",
            borderColor: "#f05b5b",
          },
          lose: {
            // 失败单元格样式
            backgroundColor: "#f2f2f2",
            color: "rgba(0, 0, 0, 0.65)",
            borderColor: "#ccc",
          },
        };
      },
    },
  },
  computed: {
    configHeight() {
      return (
        this.config.initheight +
        this.config.itemHeight +
        this.config.borderWidth
      );
    },
  },
  mounted() {},
  methods: {},
};
</script>
<style lang='scss' scoped>
.schedule {
  width: 100%;
  background-color: #fff;
  header {
    height: 36px;
    background-color: #f05b5b;
    padding-left: 20px;
    line-height: 36px;
    color: #fff;
    margin-top: 16px;
  }
  main {
    width: 100%;
    display: flex;
    border: 1px solid #e8e8e8;
    section {
      flex-grow: 1;
      // max-width: 250px;
      min-width: 150px;
      .title {
        background-color: #fdeeee;
        text-align: center;
        height: 36px;
        line-height: 36px;
      }
      .item {
        width: 100%;
        border-right: 1px dashed #e8e8e8;
        padding-left: 16px;
        padding-top: 40px;
        box-sizing: border-box;
        font-size: 12px;
        > div {
          display: flex;
          align-items: center;
        }
        section {
          height: 34px;
          position: relative;
          border: 1px solid #f05b5b;
          border-left: none !important;
          &:after {
            content: "";
            width: 30px;
            height: var(--height);
            background-color: var(--color);
            position: absolute;
            right: -30px;
            top: 50%;
            transform: translateY(-50%);
          }
          // margin-top: 40px;
          > div {
            width: 92%;
            // height: 50px;
            display: flex;
            align-items: center;
            justify-content: flex-end;
            // line-height: 48px;
            // text-align: center;
            border: 1px solid #ccc;
            position: absolute;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            background-color: #f2f2f2;
            padding-left: 16px;
            box-sizing: border-box;
            color: rgba(0, 0, 0, 0.65);
            &.win {
              background-color: rgb(250, 224, 224);
              color: #f05b5b;
              border-color: #f05b5b;
            }
          }
          > div:first-child {
            top: -14px;
            left: 0;
          }
          > div:last-child {
            bottom: -14px;
            left: 0;
          }
        }
        .winBox {
          // height: 28px;
          border: none;
          .win {
            position: relative;
            top: 0;
            left: 0;
          }
          &:after {
            content: "";
            width: 0;
            height: 0;
          }
        }
      }
    }
    section:last-child {
      .item {
        border: none;
      }
    }
  }
  .none {
    display: inline-block;
    width: 100%;
    text-align: center;
    height: 100px;
    line-height: 100px;
    background-color: #fff;
    color: #aaa;
  }
}
</style>