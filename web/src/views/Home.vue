<template>
  <div class="home">
    <div class="navigator">
      <div class="logo">
        <el-image :src="logo"/>

        <div class="divider"></div>
      </div>

      <ul class="nav-items">
        <li v-for="item in navs" :key="item.path">
          <el-tooltip
              effect="light"
              :content="item.title"
              placement="right"
          >
            <a @click="changeNav(item)" :class="item.path === curPath?'active':''">
              <i :class="'iconfont icon-'+item.icon"></i>
            </a>
          </el-tooltip>
        </li>
      </ul>
    </div>
    <div class="content">
      <router-view v-slot="{ Component }">
        <transition name="move" mode="out-in">
          <component :is="Component"></component>
        </transition>
      </router-view>
    </div>
  </div>
</template>

<script setup>

import {useRouter} from "vue-router";
import {checkSession} from "@/action/session";
import {isMobile} from "@/utils/libs";
import {ref} from "vue";

const router = useRouter();
const logo = '/images/logo.png';
const navs = ref([
  {path: "/chat", icon: "wechat", title: "对话聊天"},
  {path: "/mj", icon: "image", title: "MJ 绘画"},
  {path: "/sd", icon: "palette", title: "SD 绘画"},
  {path: "/apps", icon: "menu", title: "应用中心"},
  {path: "/images", icon: "image-list", title: "绘画社区"},
  {path: "/knowledge", icon: "book", title: "我的知识库"},
  {path: "/member", icon: "vip-user", title: "会员计划"},
  {path: "/invite", icon: "share", title: "推广计划"},
])
const curPath = ref(router.currentRoute.value.path)

const changeNav = (item) => {
  curPath.value = item.path
  router.push(item.path)
}
</script>

<style lang="stylus" scoped>
@import '@/assets/iconfont/iconfont.css';
.home {
  display: flex;
  background-color: #25272D;
  height 100vh
  width 100%

  .navigator {
    display flex
    flex-flow column
    width 48px
    padding 10px 6px
    border-right: 1px solid #3c3c3c

    .logo {
      display flex
      flex-flow column
      align-items center
      height 60px

      .divider {
        border-bottom 1px solid #4A4A4A
        width 80%
        height 10px
      }
    }

    .nav-items {
      margin-top 20px

      li {
        margin-bottom 15px

        a {
          color #DADBDC
          background-color #40444A
          border-radius 10px
          width 44px
          height 44px
          display flex
          justify-content center
          align-items center
          cursor pointer

          .iconfont {
            font-size 20px
          }
        }

        a:hover, a.active {
          color #58D3FF
        }
      }
    }
  }

  .content {
    width: 100%;
    height: 100vh;
    box-sizing: border-box;
  }

}
</style>
