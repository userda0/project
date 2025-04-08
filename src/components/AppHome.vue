<template>
  <div>
    <el-container>
      <el-aside width="200px">
        <el-menu :default-openeds="['1']">
          <el-sub-menu index="1">
            <template slot="title">菜单1</template>
            <el-menu-item v-for="(item, index) in asideData" :key="index" :index="item.value">
              {{ item.label }}
            </el-menu-item>
          </el-sub-menu>
        </el-menu>
      </el-aside>
      <el-main>
        <el-row>
          <el-col :span="24">
            <el-button type="primary" icon="el-icon-arrow-left" @click="toggleButtons">
              
            </el-button>
            <template v-if="showButtons">
              <el-button type="primary" @click="oneClickAssign" style="margin-left: 10px;">一键赋值</el-button>
              <el-button type="primary" @click="returnHome" style="margin-left: 10px;">返回主页</el-button>
              <el-button type="primary" @click="marquee" style="margin-left: 10px;">跑马灯</el-button>
              <el-button type="primary" @click="simulateScroll" style="margin-left: 10px;">模拟轮播</el-button>
              <el-select v-model="selectedVariableType" placeholder="变量类型：" style="margin-left: 10px;">
                <el-option label="Option1" value="value1"></el-option>
                <el-option label="Option2" value="value2"></el-option>
              </el-select>
              <el-input v-model="variableName" placeholder="变量名：" class="small-input" style="margin-left: 5px;"></el-input>
            </template>
          </el-col>
        </el-row>
        <el-table :data="tableData" border>
          <el-table-column label="设备代号" prop="id"></el-table-column>
          <el-table-column label="rack" prop="rack"></el-table-column>
          <el-table-column label="card" prop="card"></el-table-column>
          <el-table-column label="channel" prop="channel"></el-table-column>
          <el-table-column label="cardType" prop="cardType"></el-table-column>
          <el-table-column label="值" prop="value"></el-table-column>
          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-switch v-model="scope.row.torf" active-color="#13ce66" inactive-color="#ff4949" @change="handleSwitchChange(scope.$index)"></el-switch>
              <el-input v-model="scope.row.tovalue" style="width: 80px"></el-input>
            </template>
          </el-table-column>
        </el-table>
      </el-main>
    </el-container>
  </div>
</template>
<script>
import { Menu, Submenu, MenuItem } from 'element-ui';
const dbJson = require('@/assets/db.json');

export default {
  name: 'ElementUiExample',
  data() {
    return {
      asideData: [
        { label: 'Append', value: 'option1' },
        { label: 'Append', value: 'option2' },
        { label: 'Append', value: 'option3' }
      ],
      tableData: [],
      selectedVariableType: '',
      variableName: '',
      showButtons: true
    };
  },
  components: {
    'el-menu': Menu,
    'el-sub-menu': Submenu,
    'el-menu-item': MenuItem
  },
  mounted() {
    this.setMainData();
    // 确保DOM渲染完成后执行表头合并操作
    this.$nextTick(() => {
      // 获取表头的所有单元格
      const headerCells = document.getElementsByClassName('el-table__header')[0].rows[0].cells;
      // 将开关列（第七列，索引为6）的colspan设为2
      headerCells[6].colSpan = 2;
      // 将数值列（第八列，索引为7）的display设为none，隐藏该列的表头
      headerCells[7].style.display = 'none';
    });
  },
  methods: {
    setMainData() {
      this.tableData = dbJson.user;
    },
    simulateScroll() {
      // 模拟轮播业务逻辑代码写这里
    },
    marquee() {
      // 跑马灯业务逻辑代码写这里
    },
    returnHome() {
      // 返回主页业务逻辑代码写这里
    },
    oneClickAssign() {
      // 一键赋值业务逻辑代码写这里
    },
    toggleButtons() {
      this.showButtons = !this.showButtons;
    }
  }
};
</script>

<style scoped>
.small-input {
  width: 120px; /* 根据需要调整宽度 */
}
</style>