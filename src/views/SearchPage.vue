<template>
  <div class="nav-choose">
    <div class="search-result" v-if="searchResult">
      <div class="upload-content" v-if="store.searchValue === '0'">
        <div class="upload-title" @click="showGeneDetail">
          <span class="title">Gene:</span><span>{{ gene }}</span
          ><span class="number">{{ geneNumber }}</span>
        </div>
        <div class="dialog-basic-info common-cont">
          <el-form :model="formInfo">
            <el-form-item label="Description:">
              <div class="label">{{ formInfo.Description }}</div>
              <!-- <el-input v-model="formInfo.Description" autocomplete="off" /> -->
            </el-form-item>
            <el-form-item label="Synonyms:">
              <div class="label">{{ formInfo.Synonyms }}</div>
              <!-- <el-input v-model="formInfo.Synonyms" type="textarea" /> -->
            </el-form-item>
            <el-form-item label="Location:">
              <div class="label">{{ formInfo.Location }}</div>
              <!-- <el-input v-model="formInfo.Location" type="textarea" /> -->
            </el-form-item>
          </el-form>
        </div>
      </div>
      <p v-else-if="store.searchValue === '1'">
        <span class="title">{{ description.title }}:</span>{{ description.activeText }}
      </p>
      <p v-else-if="store.searchValue === '2'">
        <span class="title">{{ description2.title }}:</span>{{ description2.activeText }}
      </p>
    </div>
    <ul>
      <li
        v-for="(item, index) in chooseList"
        :key="item"
        @click="handleChoose(index)"
        :class="{ active: chooseIndex === index }"
      >
        {{ item }}
      </li>
    </ul>
  </div>
  <div class="result_content" v-if="searchResult">
    <search-result></search-result>
  </div>

  <!--   <div class="content">
    <div class="search-box">
      <div class="search-input">
        <el-input v-model="searchList.marker" style="width: 250px" placeholder="Please enter marker" />
        <el-input v-model="searchList.celltype" style="width: 250px" placeholder="Please enter celltype" />
        <el-input v-model="searchList.diseaseTreatment" style="width: 250px" placeholder="Please enter disease/treatment" />
      </div>
      <button @click="submitSearch">Search</button>
    </div>
    <div class="result-table">
      <el-table :data="tableData" border stripe style="width: 100%">
        <el-table-column label="project">
          <template #default="scope">
            <span class="project" @click="centerDialogVisible = true">{{ scope.row.project }}</span>
          </template>
        </el-table-column>
        <el-table-column prop="sample" label="sample" />
        <el-table-column prop="tissueCellline" label="tissue/cellline" />
        <el-table-column prop="specie" label="specie" />
        <el-table-column prop="age" label="age" />
        <el-table-column prop="sex" label="sex" />
        <el-table-column prop="diseaseTreatment" label="disease/treatment" />
        <el-table-column prop="sequence" label="sequence" />
        <el-table-column prop="source" label="source(GEO etc.)" />
        <el-table-column prop="celltypes" label="celltypes&marker" />
      </el-table>
    </div>
  </div> -->
  <project-data
    v-if="centerDialogVisible"
    @close="centerDialogVisible = false"
  ></project-data>
  <gene-detail
    v-if="geneDetailVisible"
    @close="geneDetailVisible = false"
  ></gene-detail>
</template>

<script setup lang="ts">
import ProjectData from "../components/common/ProjectData.vue";
import SearchResult from "../components/common/SearchResult.vue";
import GeneDetail from "../components/search-page/GeneDetail.vue";
import { ref, reactive, watchEffect, watch, onMounted } from "vue";
import {useStore} from '../store'
const store = useStore()
const chooseList = ref([
  "single-cell RNAseq",
  "bulk RNAseq",
  "spatial transcriptome",
  "genome",
  "proteome",
  "metabolome",
]);
const searchResult = ref(false);
const chooseIndex = ref(0);
const handleChoose = (index: number) => {
  chooseIndex.value = index;
};
const searchList = reactive({
  marker: "",
  celltype: "",
  diseaseTreatment: "",
});
const submitSearch = () => {
  console.log(
    searchList.marker,
    searchList.celltype,
    searchList.diseaseTreatment
  );
};
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
// const active = ref(0);
const gene = ref("RUNX1");
const geneNumber = ref("(ENSG00000163699)");
const centerDialogVisible = ref(false);
const formInfo = reactive({
  Description: "",
  Synonyms: "",
  Location: "",
});
const description = ref({
  title: "B cell Description",
  activeText: `在肺组织中，B细胞（B cell）是关键的免疫细胞，属于适应性免疫系统
  的一部分，负责抗体的产生和体液免疫的调控。肺部的B细胞在感染和炎症过程中发挥着重要作用，
  尤其是在抵抗病毒、细菌等病原体的入侵时`,
});
const description2 = ref({
  title: "IPF Description",
  activeText: `特发性肺纤维化（Idiopathic Pulmonary Fibrosis，IPF）是一种慢性、进行性、不可逆的间质性肺疾病，
  其特征是肺泡和肺间质的纤维化，导致肺组织逐渐硬化和失去功能。IPF的病因尚不完全清楚，
  因此称为“特发性”，通常发生在中老年人群中，且男性发病率略高于女性。`,
});
/* const change = () => {
  if(active.value===0){
    active.value = 1;
    store.status2 = true
  }else{
    active.value = 0;
  }
}; */
const geneDetailVisible = ref(false);
const showGeneDetail = () => {
  geneDetailVisible.value = true;
};
watch(()=> store.status, (newVal, oldVal) => {
  console.log('store',store.status,newVal, oldVal)
  searchResult.value = store.status
})
onMounted(() => {
  console.log('store',store.status)
  searchResult.value = store.status
})
</script>
<style scoped lang="scss">
$color-red: #6d1d29;
$color-blue: #254682;
$color-baby-blue: #365baa;
@mixin size($width, $height) {
  width: $width;
  height: $height;
}
@mixin layout($align, $justify) {
  display: flex;
  align-items: $align;
  justify-content: $justify;
}
.search-result {
  width: 100%;
  height: auto;
  .upload-content {
    //margin: 20px 0;
    @include layout(flex-start, center);
    flex-direction: column;
    .icon {
      width: 100%;
      font-size: 25px;
      color: #9f9f9f;
      i {
        font-size: 70px;
        color: #9f9f9f;
      }
    }
    .upload-title {
      font-size: 20px;
      margin: 20px 0;
      font-weight: bold;
      cursor: pointer;
      .number {
        font-size: 16px;
      }
      &:hover{
        color: #254682;
      }
    }
    .dialog-basic-info {
      @include size(100%, auto);
      .el-form {
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        border: 1px dashed #b3b3b34d;
        padding: 20px 20px 10px;
        box-sizing: border-box;
        border-radius: 10px;
        .el-form-item {
          width: 100%;
          margin-bottom: 10px;
          :deep .el-form-item__label {
            width: 100px;
            justify-content: flex-start;
            font-weight: bold;
          }
          .el-form-item__content {
            width: calc(100% - 100px);
          }
          .label {
            border: 1px dashed #b3b3b336;
            padding: 0 20px;
            border-radius: 5px;
            width: calc(100% - 0px);
            text-align: left;
            height: 32px;
          }
        }
      }
    }
  }
  p {
    font-size: 17px;
    text-align: left;
    padding: 15px 20px;
    box-shadow: 0 0px 4px 1px rgba(0, 0, 0, 0.06);
    border-radius: 5px;
    .title{
      font-weight: bold;
      padding-right: 10px;
    }
  }
}
.nav-choose {
  width: 100%;
  height: auto;
  box-sizing: border-box;
  border-radius: 5px;
  // border: 1px solid #e6e6e6;
  margin: 20px 0;
  display: flex;
  flex-direction: column;
  ul {
    width: 100%;
    padding: 20px 0;
    li {
      width: auto;
      background-color: #ededed;
      color: #4d4d4d;
      padding: 5px 15px;
      border-radius: 5px;
      cursor: pointer;
      margin-right: 15px;
      font-size: 19px;
      &:hover {
        background-color: $color-baby-blue;
        color: white;
      }
      &:last-child {
        margin: 0;
      }
    }
    .active {
      background-color: $color-blue;
      color: white;
    }
    @include layout(center, flex-start);
  }
  @include layout(center, flex-start);
}
.result_content {
  width: 100%;
}
.content {
  width: 100%;
  border: 1px solid #e6e6e6;
  border-radius: 5px;
  padding: 20px;
  box-sizing: border-box;
  .search-box {
    width: 100%;
    height: 80px;
    box-sizing: border-box;
    .search-input {
      :deep .el-input {
        margin-right: 10px;
        height: 40px;
      }
    }
    @include layout(center, space-between);
    button {
      outline: none;
      color: white;
      background-color: $color-baby-blue;
      border: none;
      border-radius: 5px;
      font-size: 15px;
      padding: 5px 10px;
      &:hover {
        background-color: $color-blue;
      }
    }
  }
  .result-table {
    /*    :deep .el-table .el-table__cell{
      padding: 0;
    }*/
    .dialog {
      width: 100%;
      height: 100%;
      position: fixed;
      top: 0;
      left: 0;
      background-color: rgba(56, 52, 52, 0.62);
      z-index: 3;
      @include layout(center, center);
      .dialog-inner {
        width: 80%;
        height: 80%;
        background-color: white;
        border-radius: 10px;
        .dialog-top {
          height: 50px;
          border-bottom: 1px solid #e6e6e6;
          padding: 0 30px;
          @include layout(center, space-between);
          .iconfont {
            cursor: pointer;
          }
        }
        .common-cont {
          width: 100%;
          padding: 30px;
          box-sizing: border-box;
          .title {
            text-align: left;
            padding-bottom: 10px;
          }
        }
        .dialog-basic-info {
          height: auto;
          .el-form {
            width: 100%;
            display: flex;
            flex-wrap: wrap;
            border: 1px dashed #b3b3b3;
            padding: 20px 20px 10px;
            box-sizing: border-box;
            border-radius: 10px;
            .el-form-item {
              width: 45%;
              margin-right: 10%;
              margin-bottom: 10px;
              :deep .el-form-item__label {
                width: 150px;
                justify-content: flex-start;
                font-weight: bold;
              }
              .el-form-item__content {
                width: calc(100% - 150px);
              }
              .label {
                border: 1px dashed #b3b3b3;
                padding: 0 20px;
                border-radius: 5px;
                width: calc(100% - 0px);
                text-align: left;
              }
              &:nth-child(2n) {
                margin-right: 0;
              }
              &:last-child {
                width: 100%;
                margin-right: 0;
                .label {
                  line-height: 1.5;
                  padding: 10px 20px;
                }
              }
            }
          }
        }
        .dialog-content {
          .bottom-content {
          }
        }
      }
    }
    .data-detail {
      width: 90%;
      height: 90%;
    }
  }
}
</style>
