<template>
  <div class="search_choose">
    <div class="single_choose" v-for="item in formInfo">
      <el-select v-model="item.Species" v-if="!item.disabled">
        <el-option
          v-for="list in item.SpeciesList"
          :key="list.value"
          :label="list.label"
          :value="list.value"
        />
      </el-select>
      <span class="no_choose" v-if="item.disabled">{{ item.Species }}</span>
    </div>
  </div>
  <div class="dataset">
    <div class="dataset_title">Dataset 1</div>
    <p>
      {{ datasetDetail }}
      <span style="color: #ad001a; font-size: 18px; cursor: pointer;" @click="goToProject">【Go to its project】</span>
    </p>
    <div class="chart_table">
      <div class="chart_table_inner">
        <div class="top_nav">
          <span :class="{nav_active:activeName==='chart'}" @click="()=>{activeName='chart'}"><i class="iconfont icon-renkou"></i>chart</span>
          <span :class="{nav_active:activeName==='data'}" @click="()=>{activeName='data'}"><i class="iconfont icon-shijieyeshengdongwuri"></i>data</span>
        </div>
        <div v-if="activeName === 'chart'">
          <home-echarts
            :sortType="'Human'"
            v-if="activeName === 'chart' && store.searchValue === '1'"
          ></home-echarts>
          <img v-else style="width: 80%;" :src="charts" alt="" />
        </div>
        <div v-else-if="activeName === 'data'" class="result_table">
            <el-table :data="tableData" border stripe style="width: 100%">
              <el-table-column prop="sample" label="sample" />
              <el-table-column prop="tissueCellline" label="tissue/cellline" />
              <el-table-column prop="specie" label="specie" />
              <el-table-column prop="age" label="age" />
              <el-table-column prop="sex" label="sex" />
              <el-table-column
                prop="diseaseTreatment"
                label="disease/treatment"
              />
              <el-table-column prop="sequence" label="sequence" />
              <el-table-column prop="source" label="source(GEO etc.)" />
              <el-table-column prop="celltypes" label="celltypes&marker" />
            </el-table>
        </div>
      </div>
<!--       <el-tabs
        type="border-card"
        v-model="activeName"
        class="demo-tabs"
        @tab-click="handleClick"
      >
        <el-tab-pane name="chart">
          <template #label>
            <span class="custom-tabs-label">
              <i class="iconfont icon-renkou"></i>
              <span>Chart</span>
            </span>
          </template>
          <home-echarts
            :sortType="'Human'"
            v-if="activeName === 'chart' && store.searchValue === '1'"
          ></home-echarts>
          <img v-else style="width: 80%;" :src="charts" alt="" />
        </el-tab-pane>
        <el-tab-pane name="table">
          <template #label>
            <span class="custom-tabs-label">
              <i class="iconfont icon-shijieyeshengdongwuri"></i>
              <span>Data</span>
            </span>
          </template>
          <div class="result-table">
            <el-table :data="tableData" border stripe style="width: 100%">
              <el-table-column prop="sample" label="sample" />
              <el-table-column prop="tissueCellline" label="tissue/cellline" />
              <el-table-column prop="specie" label="specie" />
              <el-table-column prop="age" label="age" />
              <el-table-column prop="sex" label="sex" />
              <el-table-column
                prop="diseaseTreatment"
                label="disease/treatment"
              />
              <el-table-column prop="sequence" label="sequence" />
              <el-table-column prop="source" label="source(GEO etc.)" />
              <el-table-column prop="celltypes" label="celltypes&marker" />
            </el-table>
          </div>
        </el-tab-pane>
      </el-tabs> -->
    </div>
  </div>

  <project-data v-if="showProjectData" @close="showProjectData = false"></project-data>
</template>
<script setup lang="ts">
import { set } from "lodash";
import HomeEcharts from "./HomeEcharts.vue";
import ProjectData from "./ProjectData.vue";
import { reactive, ref, watch } from "vue";
import { useStore } from "../../store";
import image from "../../assets/image.png";
import image2 from "../../assets/image2.png";
const store = useStore();
const formInfo = reactive([
  {
    Species: "Human",
    disabled: false,
    SpeciesList: [
      { value: "Human", label: "Human" },
      { value: "Animal models", label: "Animal models" },
    ],
  },
  {
    Species: "Disease",
    disabled: false,
    SpeciesList: [
      { value: "Disease", label: "Disease" },
      { value: "Health", label: "Health" },
      { value: "IPF", label: "IPF" },
    ],
  },
  {
    Species: "Lung",
    disabled: false,
    SpeciesList: [
      { value: "Lung", label: "Lung" },
      { value: "Blood", label: "Blood" },
    ],
  },
  {
    Species: "B Cell",
    disabled: false,
    SpeciesList: [
      { value: "All Cell types", label: "All Cell types" },
      { value: "B Cell", label: "B Cell" },
    ],
  },
]);
const datasetDetail =
  ref(`Dataset 1 description Dataset 1 description Dataset 1 description Dataset 1 description Dataset 1 
    description Dataset 1 description Dataset 1 description Dataset 1 description Dataset 1 description Dataset 1 
    description Dataset 1 description Dataset 1 description `);
const tableData = [
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
  {
    project: "LPS00001",
    sample: "No. 189, Grove St, Los Angeles",
    tissueCellline: "No.Angeles",
    specie: "No.Angeles",
    age: 35,
    sex: "男",
    diseaseTreatment: "sdg",
    sequence: "sdg",
    source: "sdg",
    celltypes: "sdg",
  },
];
const activeName = ref("chart");
const handleClick = (tab: { paneName: string }, event: any) => {
  console.log(112, tab, event);
  setTimeout(() => {
    activeName.value = tab.paneName;
    console.log(11, activeName.value);
  }, 1000);
};
const showProjectData = ref(false);
const goToProject = () => {
  showProjectData.value = true;
};
/* const searchResultList = ref([
  {
    title: 'Dataset 1',
  }
]); */
const charts = ref(image)
watch(
  () => store.searchValue,
  (newVal, oldVal) => {
    console.log("store--------", store.searchValue, newVal, oldVal);
    if (store.searchValue === "0") {
      formInfo[0].disabled = false;
      formInfo[1].disabled = false;
      formInfo[2].disabled = false;
      formInfo[3].disabled = false;
      charts.value = image
    } else if (store.searchValue === "1") {
      formInfo[0].disabled = false;
      formInfo[1].disabled = false;
      formInfo[2].disabled = false;
      formInfo[3].disabled = true;
      charts.value = image2;
    } else if (store.searchValue === "2") {
      formInfo[0].disabled = false;
      formInfo[1].disabled = true;
      formInfo[1].Species = 'IPF';
      formInfo[2].disabled = false;
      formInfo[3].disabled = false;
      charts.value = image
    }
  },
  {
    immediate: true,
  }
);
</script>
<style scoped lang="scss">
.search_choose {
  display: flex;
  .single_choose {
    display: flex;
    align-items: center;
    &::after {
      content: "";
      display: block;
      width: 10px;
      height: 2px;
      background-color: #4d4d4d;
      border-radius: 15px;
      margin: 0 10px;
    }
    &:last-child::after {
      display: none;
    }
  }
  :deep .el-select {
    font-weight: 600;
    width: 200px;
  }
  .no_choose {
    font-size: 18px;
    font-weight: 600;
    display: flex;
    align-items: center;
  }
}
.dataset {
  box-shadow: 0 0px 5px 1px rgb(0 0 0 / 6%);
  // padding: 20px;
  box-sizing: border-box;
  border-radius: 3px;
  margin-top: 15px;
  border: 1px solid #dcdfe68a;
  .dataset_title{
    background-color: #adb8c9;
    color: white;
  }
  p {
    text-align: left;
    font-size: 18px;
    padding: 0 20px
  }
  .chart_table{
    padding: 0 20px 20px;
    .chart_table_inner{
      border: 1px solid #dcdfe68a;
      .top_nav{
        display: flex;
        align-items: center;
        justify-content: flex-start;
        background-color: #f5f7fa;
        span{
          font-size: 18px;
          cursor: pointer;
          padding: 6px 15px;;
          &:hover{
            color: #0043d3;
          }
          &:first-child{
            border-right: 1px solid #dcdfe68a;
          }
        }
        .nav_active{
          color: #0043d3;
          background-color: white;
        }
      }
      .result_table{
        padding: 15px;
      }
    }
  }
}
</style>
