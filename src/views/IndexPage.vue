<template>
  <div class="common-layout">
    <header>
      <div class="header-outer">
        <div class="header-content">
          <div class="header-bg"></div>
          <div class="logo" @click="handleChoose('/', 0)">
            <img src="../assets/logo.png" alt="" />
          </div>
          <div class="nav">
            <ul class="nav-list">
              <li
                class="menu_item"
                v-for="(item, index) in navList"
                :key="item.name"
                @click="handleChoose(item.path, index)"
                :class="{ active: chooseIndex === index }"
              >
                {{ item.name }}
              </li>
            </ul>
            <div class="middle-content">
              <i class="iconfont icon-zhongyingwenqiehuan-yingwen"></i>
              <i class="iconfont icon-denglu" @click="Login"></i>
            </div>
          </div>
        </div>
      </div>
      <div class="system-name">
        <p>{{ systemName }}</p>
        <div class="search">
          <input type="text" v-model="searchInput" />
          <!--          <div class="search-button">{{search}}</div>-->
          <i class="iconfont icon-linedesign-12" @click="showSearchResult(searchInput)"></i>
        </div>
        <div class="example" v-if="router.currentRoute.value.path.includes('/search')">
          e.g.: <span @click="showSearchResult('0')">RUNX1</span><span @click="showSearchResult('1')">B cell</span><span @click="showSearchResult('2')">IPF</span>
        </div>
      </div>
    </header>
    <main><router-view></router-view></main>
    <footer>
      <div class="footer-content">
        <div class="footer-left">
          <p>
            Supported by the National Heart, Lung, and Blood Institute of the
            National Institutes of Health
          </p>
          <p>under Award Number U24HL148865</p>
          <p>©2022 CCHMC based upon ©2017 RTI International</p>
        </div>
        <div class="footer-right">
          <div class="common">
            <i class="iconfont icon-feiniao"></i>
          </div>
          <div class="common">
            <i class="iconfont icon-tianchongxing-"></i>
          </div>
        </div>
      </div>
    </footer>
  </div>
  <div class="popover" v-if="visible">
    <!-- <el-popover :visible="visible" placement="right" style="position:absolute; right: 0 !important; bottom: 0; z-index: 1000;" :width="250" popper-class="special-popover"> -->
    <span>用户A请求下载用户B的XXX文件，请确认是否同意？</span>
    <div style="text-align: right; margin-top: 10px">
      <el-button size="small" type="primary" @click="visible = false">
        同意
      </el-button>
      <el-button size="small" text @click="visible = false">不同意</el-button>
    </div>
    <!-- </el-popover> -->
  </div>
  <!--   <el-popover :visible="visible" placement="right" :width="160" popper-class="special-popover">
    <p>Are you sure to delete this?</p>
    <div style="text-align: right; margin: 0">
      <el-button size="small" text @click="visible = false">cancel</el-button>
      <el-button size="small" type="primary" @click="visible = false">
        confirm
      </el-button>
    </div>
    <template #reference>
      <el-button @click="visible = true"></el-button>
    </template>
  </el-popover> -->
  <login-page v-if="gotoLoginPage" @close="gotoLoginPage = false"></login-page>
</template>
<script setup lang="ts">
import { ref, watchEffect, onMounted } from "vue";
import router from "../router";
import LoginPage from "./LoginPage.vue";
// import { ElNotification } from 'element-plus'
import { useStore } from "../store";
const store = useStore();
const systemName = ref<String>("Researches and Bio-resources of Lung Disease");
const navList = ref([
  { name: "Home", path: "/", label: "/home", order: 0 },
  { name: "Search", path: "/search", label: "/search", order: 1 },
  { name: "Tools", path: "/tools", label: "/tools", order: 2 },
  { name: "Project", path: "/project", label: "/project", order: 3 },
  { name: "Help", path: "/help", label: "/help", order: 4 },
]);
const searchInput = ref("");
const showSearchResult = (value: string) => {
  store.status = true;
  store.searchValue = value;
  console.log("search", store);
};
const gotoLoginPage = ref(false);
const visible = ref(true);
const Login = () => {
  gotoLoginPage.value = true;
};
const chooseIndex = ref(0);
const handleChoose = (path: any, index: number) => {
  router.push(path);
  chooseIndex.value = index;
};
watchEffect(() => {
  let item = navList.value.find((item) => {
    if (router.currentRoute.value.path.includes(item.label)) {
      return router.currentRoute.value.path.includes(item.label);
    }
  });
  chooseIndex.value = item ? item.order : 0;
});
onMounted(() => {
  /*  let user = '管理员'
  if (user === '管理员') {
    ElNotification({
      title: 'tips',
      dangerouslyUseHTMLString: true,
      message: `<strong>用户A请求下载用户B的XXX文件，请确认是否同意？
              <options style="display: flex;justify-content: flex-end">
                <option value="1" style="cursor: pointer;color: #365baa">同意</option>
                <option value="2" style="cursor: pointer;color: #6d1d29;margin-left: 10px">不同意</option>
              </options>
              </strong>`,
      position: 'bottom-right',
      duration: 0,
      type: 'info',
    })
  }*/
});
</script>
<style scoped lang="scss">
$color-red: #6d1d29;
$color-blue: #365baa;
@mixin layout($align, $justify) {
  display: flex;
  align-items: $align;
  justify-content: $justify;
}
@mixin max-width() {
  width: 80%;
  max-width: 1920px;
  margin: 0 auto;
}
.common-layout {
  width: 100%;
  height: 100%;
  header {
    height: 300px;
    background-color: #fff;
    border-bottom: 1px solid #d7d7d7;
    position: relative;
    isolation: isolate;
    color: #e0e0e0;
    .header-bg {
      width: 100%;
      height: 100%;
      background-image: url("../assets/header-bg.png");
      background-size: cover;
      background-position: center;
      position: absolute;
      top: 0;
      left: 0;
      z-index: -1;
    }
    .header-outer {
      width: 100%;
      height: 100px;
      background-color: rgba(0, 0, 0, 0.06);
      box-shadow: 0px 1px 14px 5px #00000021;
      .header-content {
        height: 100%;
        @include max-width();
        @include layout(center, space-between);
        .logo {
          height: 100%;
          cursor: pointer;
          img {
            height: 70px;
            padding: 15px 0;
          }
        }
        .nav {
          height: 100%;
          @include layout(center, space-between);
          .nav-list {
            height: 100%;
            @include layout(center, space-between);
            .menu_item {
              height: 100%;
              padding: 0 20px;
              cursor: pointer;
              position: relative;
              transition: ease all 0.5s;
              font-size: 22px;
              @include layout(center, center);
              &:hover {
                color: white;
                &::after {
                  width: 30%;
                  height: 3px;
                  position: absolute;
                  left: 50%;
                  bottom: 0px;
                  border-radius: 50px;
                  background: white;
                  content: "";
                  -webkit-transition: all 0.35s;
                  color: white;
                  transform: translate(-50%);
                  transition: ease all 0.5s;
                }
              }
            }
            .active {
              color: white;
              position: relative;
              &::after {
                width: 30%;
                height: 3px;
                position: absolute;
                left: 50%;
                bottom: 0px;
                border-radius: 50px;
                background: white;
                content: "";
                -webkit-transition: all 0.35s;
                color: white;
                transform: translate(-50%);
              }
            }
          }
          .middle-content {
            i {
              font-size: 26px;
              cursor: pointer;
              padding-left: 20px;
            }
          }
        }
      }
    }
    .system-name {
      height: calc(100% - 100px);
      font-size: 40px;
      font-weight: bold;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      color: #ffffff;
      p {
        margin-top: 0;
        margin-bottom: 15px;
      }
      .search {
        width: 40%;
        max-width: 800px;
        height: 40px;
        display: flex;
        position: relative;
        border-radius: 0 40px 40px 0;
        overflow: hidden;
        padding-right: 5px;
        input {
          width: 99%;
          background-color: #f7f7f738;
          border: 1px solid #d9d9d9;
          position: absolute;
          left: 0;
          top: 0;
          height: 100%;
          padding: 0 60px 0 20px;
          font-size: 16px;
          color: #333;
          outline: none;
          box-sizing: border-box;
          margin-left: 2px;
          border-radius: 40px;
        }
        /*        .search-button{
          position: absolute;
          top: 0;
          right: 0;
          width: 80px;
          height: 100%;
          background-color: #0077aa;
          color: white;
          @include layout(center,center);
        }*/
        .iconfont {
          position: absolute;
          top: 5px;
          right: 15px;
          font-size: 20px;
          color: #606060;
          background-color: white;
          height: 30px;
          aspect-ratio: 1;
          border-radius: 30px;
          cursor: pointer;
          @include layout(center, center);
        }
      }
      .example {
        font-size: 17px;
        font-weight: 400;
        margin-top: 10px;
        width: 40%;
        max-width: 800px;
        text-align: left;
        color: white;
        span {
          border-bottom: #ffffff solid 1px;
          margin-right: 15px;
          cursor: pointer;
        }
      }
    }
  }
  main {
    height: auto;
    min-height: calc(100% - 480px);
    @include max-width();
    margin-bottom: 28px;
  }
  footer {
    height: 150px;
    width: 100%;
    background-color: #f5f5f5;
    border-top: 1px solid #d7d7d72b;
    margin: 0 auto;
    margin-top: 100px;
    .footer-content {
      @include layout(center, space-between);
      @include max-width();
      .footer-left {
        text-align: left;
        p {
          font-size: 14px;
          color: #666;
          margin-botto: 0;
        }
      }
      .footer-right {
        display: flex;
        flex-direction: column;
        .common {
          width: 50px;
          height: 50px;
          margin: 10px 0;
          border-radius: 50%;
          background-color: #fff;
          @include layout(center, center);
        }
        i {
          font-size: 30px;
          color: #666;
        }
      }
    }
  }
}
:deep options {
  @include layout(center, flex-end);
  option {
    cursor: pointer;
  }
}
:deep option {
  color: red;
}
.popover {
  width: 250px;
  height: auto;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 1px 2px 10px 3px #0000001c;
  position: fixed;
  right: 20px;
  bottom: 20px;
  z-index: 1000;
  padding: 20px;
  text-align: left;
  font-size: 16px;
}
:deep .special-popover {
  position: absolute;
  right: 20px;
  bottom: 20px;
}
:deep .el-popover.el-popper {
  position: absolute;
  right: 20px !important;
  bottom: 20px !important;
  width: 250px;
}
</style>
