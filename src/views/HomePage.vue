<template>
  <div class="container">
    <div class="basic-info common-section">
      <div class="about" id="introduction">
        <h3>About</h3>
        <div class="content">
          {{ introduction }}
        </div>
      </div>
      <div class="right-side" id="images">
        <!-- <div class="images" id="images">
            <img alt="" v-for="(image,index) in images" :key="index" :src="image">
        </div> -->
        <div class="icons">
          <div
            class="icon-container"
            @click="chooseSort('1')"
            :class="{ active: sortType === '1' }"
          >
            <i class="iconfont icon-Humanresources"></i>
            <span>Human</span>
          </div>
          <div
            class="icon-container"
            @click="chooseSort('2')"
            :class="{ active: sortType === '2' }"
          >
            <i class="iconfont icon-animal1"></i>
            <span>Animal models </span>
          </div>
        </div>
        <div class="contant" id="content">
          <div class="content_inner">
            <div class="custom-tabs">
              <div class="single" v-if="sortType === '1'">
                <!--               <div class="custom-tabs-label">
                <i class="iconfont icon-renkou"></i><span>Human</span>
              </div> -->
                <el-tree
                  class="filter-tree"
                  :data="humanTreeData"
                  :props="defaultProps"
                  default-expand-all
                />
              </div>
              <div class="single" v-else-if="sortType === '2'">
                <!--          <div class="custom-tabs-label">
                <i class="iconfont icon-shijieyeshengdongwuri"></i
                ><span>Animal models </span>
              </div> -->
                <el-tree
                  class="filter-tree"
                  :data="animalTreeData"
                  :props="defaultProps"
                  default-expand-all
                />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="data-statistics common-section">
      <h3>Data Statistics</h3>
      <div class="echarts-container">
        <div
          class="echarts-item"
          v-for="(item, index) in dataStatistics"
          :key="index"
        >
          <i class="iconfont" :class="item.icon"></i>
          <span class="count">{{ item.count }}</span
          ><span class="title">{{ item.title }}</span>
        </div>
      </div>
    </div>
    <div class="news-section common-section">
      <h3>News</h3>
      <div class="news-container">
        <div class="news-item"></div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import myImage from "../assets/fenzi.png";
import myImage2 from "../assets/fei.png";
import myImage3 from "../assets/xianliti.png";
import myImage4 from "../assets/fenzi.png";
const introduction =
  ref(`Welcome to our Lung Multi-Omics Database (LMOD), an initiative meticulously curated by Laboratory of Pulmonary Immunology and Inflammation,
    Frontiers Science Center for Disease-related Molecular Network, West China Hospital, Sichuan University. Our repository is dedicated to the advancement of understanding in pulmonary immunology and inflammatory processes.
    The scope of our investigative pursuits encompasses the 1) intricate phenomena of pulmonary senescence, 2) the pathophysiological intricacies of Interstitial Lung Disease (ILD) as well as Chronic Obstructive Pulmonary Disease (COPD), 3)
    dovetailing into the pivotal role of mitochondrial function within the pulmonary milieu.
    This compendium serves as a platform to disseminate our research insights and to amalgamate a wealth of multi-omic datasets pertinent to lung health and disease. We invite the academic community to collaborate and utilize our database,
    accessible through a seamless download interface. We are receptive to intellectual discourse and welcome any inquiries or propositions for the enhancement of this knowledge base.
    `);
const images = ref([myImage, myImage2, myImage3, myImage4]);
interface Tree {
  [key: string]: any;
}
const defaultProps = {
  children: "children",
  label: "label",
};
const humanTreeData: Tree[] = [
  {
    id: 1,
    label: "Health(1000)",
    children: [
      {
        id: 4,
        label: "Aging(1000)",
        children: [
          {
            id: 9,
            label: "Young(310)",
          },
          {
            id: 10,
            label: "Middle-aged(300)",
          },
          {
            id: 11,
            label: "Old(390)",
          },
        ],
      },
    ],
  },
  {
    id: 2,
    label: "Disease(900)",
    children: [
      {
        id: 5,
        label: "ILAD(300)",
      },
      {
        id: 6,
        label: "ILD(300)",
        children: [
          {
            id: 9,
            label: "myositis-ILD(310)",
          },
          {
            id: 10,
            label: "ssc-ILD(300)",
          },
          {
            id: 11,
            label: "rare-ILD(390)",
          },
        ],
      },
      {
        id: 7,
        label: "IPF(300)",
      },
      {
        id: 8,
        label: "Sarcoidosis(300)",
      },
      {
        id: 9,
        label: "Other_diseases(300)",
      },
    ],
  },
];
const animalTreeData: Tree[] = [
  {
    id: 1,
    label: "Mouse(1000)",
    children: [
      {
        id: 4,
        label: "Mouse cre-geneA(1000)",
      },
      {
        id: 4,
        label: "Mouse si-geneB(1000)",
      },
      {
        id: 4,
        label: "BLM mouse(1000)",
      },
      {
        id: 4,
        label: "Low-oxygen mouse(1000)",
        children: [
          {
            id: 9,
            label: "Blood(310)",
          },
          {
            id: 10,
            label: "Lung(300)",
          },
          {
            id: 11,
            label: "X cellline knock geneC(390)",
          },
        ],
      },
    ],
  },
  {
    id: 2,
    label: "Monkey(900)",
    children: [
      {
        id: 6,
        label: "Aging(300)",
        children: [
          {
            id: 9,
            label: "Young(310)",
          },
          {
            id: 10,
            label: "Middle-aged(300)",
          },
          {
            id: 11,
            label: "Old(390)",
          },
        ],
      },
      {
        id: 7,
        label: "Pig(300)",
      },
    ],
  },
];
const sortType = ref<string>("1");
const chooseSort = (type: string) => {
  sortType.value = type;
  console.log(sortType.value);
};
const dataStatistics = ref([
  {
    icon: "icon-Project-projects",
    title: "Projects",
    count: 1000,
  },
  {
    icon: "icon-species",
    title: "Species",
    count: 1000,
  },
  {
    icon: "icon-Cells",
    title: "Cells",
    count: 1000,
  },
  {
    icon: "icon-xibaocells",
    title: "Cell types",
    count: 1000,
  },
  {
    icon: "icon-education-research-_experiment-samples",
    title: "Samples",
    count: 1000,
  },
  {
    icon: "icon-zhitutubiao_tianjiazhibeizhen",
    title: "Treatment/Diseases",
    count: 1000,
  },
]);
const handleResize = () => {
  if (window.innerWidth > 1300 && window.innerWidth < 1975) {
    console.log("resize", window.innerWidth);
    (document as any).getElementById("images").style.height = `${
      (document as any).getElementById("introduction").clientHeight
    }px`;
  }
  /*   (document as any).getElementById("content").style.height =
    (document as any).getElementById("images").clientHeight - 90 + "px"; */
};
onMounted(() => {
  console.log("resize22", window.innerWidth);
  /*   (document as any).getElementById("images").style.height = `${
    (document as any).getElementById("introduction").clientHeight
  }px`; */
  handleResize();
  window.addEventListener("resize", handleResize);
});
onUnmounted(() => {
  window.removeEventListener("resize", handleResize);
});
</script>
<style scoped lang="scss">
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
.container {
  width: 100%;
  display: flex;
  flex-direction: column;
  .common-section {
    margin-top: 50px;
    text-align: left;
  }
  .basic-info {
    @include layout(flex-start, space-between);
    box-shadow: 0 2px 10px 1px #0000000d;
    padding: 20px;
    .about {
      text-align: left;
      .content {
        font-size: 18px;
      }
      h3 {
        margin-top: 0px;
      }
    }
    .right-side {
      box-shadow: 3px 3px 12px 2px #b7b7b780;
      background-color: #efefef9c;
      .icons {
        border-bottom: 1px solid #ededed;
        display: flex;
        @include layout(center, space-around);
        .icon-container {
          width: calc(50% - 1px);
          cursor: pointer;
          color: #616161;
          @include layout(center, flex-start);
          padding-left: 20px;
          font-size: 22px;
          .iconfont {
            font-size: 28px;
            margin-right: 10px;
          }
          &:first-child {
            border-right: 1px solid #ededed;
          }
        }
        .active {
          color: #365baa;
          // background-color: #254682;
        }
      }
      .contant {
        padding: 20px;
        .content_inner {
          width: 100%;
          height: auto;
          min-height: 300px;
          background-color: white;
          padding: 10px;
          box-sizing: border-box;
        }
      }
      /*       margin-top: 75px;
      @include layout('',flex-end);
      .images{
        width: 85%;
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-end;
        border-radius: 5px;
        img {
          aspect-ratio: 1.5;
          object-fit: cover;
          border-radius: 5px;
          height: calc(50% - 5px);
          max-width: calc(50% - 5px);
          &:nth-child(odd) {
            margin-right: 10px;
          }
          &:nth-child(3), &:nth-child(4) {
            margin-top: 10px;
          }
        }
      } */
    }
  }
  .sort-section {
    .custom-tabs {
      @include layout(flex-start, space-between);
      box-shadow: 1px 2px 15px 1px #7979791a;
      border-radius: 5px;
      .single {
        width: calc(50% - 1px);
        padding: 15px 20px;
        box-sizing: border-box;
        border-right: 1px solid #bbbbbb2e;
        .custom-tabs-label {
          font-size: 22px;
          padding-bottom: 10px;
          .iconfont {
            margin-right: 10px;
            font-size: 22px;
          }
          span {
            font-weight: bold;
          }
        }
        &:last-child {
          border-right: none;
        }
      }
    }
  }
  .data-statistics {
    .echarts-container {
      display: flex;
      flex-wrap: wrap;
      background-color: rgb(249 249 249);
      border-radius: 5px;
      padding: 20px 25px;
      .echarts-item {
        width: calc(100% / 3);
        @include layout(center, flex-start);
        .iconfont {
          font-size: 40px;
          color: #254682;
          margin-right: 15px;
        }
        .count {
          font-size: 17px;
          color: #6d1d29;
          margin-right: 5px;
        }
        .title {
          font-size: 17px;
          color: #254682;
        }
      }
    }
  }
}
@media screen and (min-width: 1301px) {
  .about {
    width: 50%;
  }
  .right-side {
    min-width: 460px;
    max-width: 600px;
    margin: 10px 15px;
    width: 40%;
  }
}
@media screen and (max-width: 1300px) {
  .basic-info {
    flex-direction: column;
  }
  .about {
    width: 100%;
  }
  .right-side {
    width: 100%;
    margin: 20px 0;
  }
}
</style>
