<template>
  <table class="basic-table">
    <tbody>
      <tr v-for="(tds, index) of props.data" :key="index">
        <td
          v-for="(td, subIndex) of tds"
          :key="subIndex"
          :colspan="td.colspan"
          :class="td.isTh && 'th'"
        >
          <!--优先级：插槽 >  text-->
          <slot v-if="td.slotName" :name="td.slotName" :text="td.text"></slot>
          <template v-else>{{ td.text }}</template>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup lang="ts">
type Td = {
  isTh: boolean;
  text: string;
  colspan?: number;
  slotName?: string;
};

type Tr = Td[];

type TableData = Tr[];

type TableConfig = {
  key: string;
  name: string;
  colspan?: number;
  slotName?: string;
};

const props = defineProps<{
  data: TableData;
}>();

function getBasicData(
  fieldValue: Record<string, any>,
  tableConfig: TableConfig[]
) {
  const list: Td[] = [];
  tableConfig.forEach((item) => {
    // th数据
    const th = {
      isTh: true,
      colspan: 1,
      text: item.name,
    };
    // td数据
    const td = {
      isTh: false,
      colspan: item.colspan || 1,
      text: fieldValue[item.key],
    };

    item.slotName && Object.assign(td, { slotName: item.slotName });

    list.push(th, td);
  });

  return list;
}

function handleBasicData(target: Td[], colNum: number, tableData: TableData) {
  let sum = 0;
  let deleteCount = 0;
  const listItem: Tr = [];
  for (let i = 0; i < target.length; i++) {
    if (sum < colNum) {
      const item = target[i];
      listItem.push(item);
      sum += item.colspan || 1;
      deleteCount++;
    } else {
      break;
    }
  }
  listItem.length && tableData.push(listItem);
  target.length > 0 &&
    handleBasicData(target.splice(0, deleteCount) && target, colNum, tableData);
}

function getTableData(
  fieldValue: Record<string, any>,
  tableConfig: TableConfig[],
  colNum: number
) {
  const tableData: TableData = [];
  const basicData = getBasicData(fieldValue, tableConfig);
  handleBasicData(basicData, colNum, tableData);
  return tableData;
}

defineExpose({
  getTableData,
});
</script>

<script lang="ts">
export default {
  name: "BasicTable",
};
</script>

<style scoped lang="less">
.basic-table {
  width: 100%;
  border-collapse: collapse;
  border: 1px solid #edf1f6;

  td {
    border: 1px solid #edf1f6;
    //border-bottom: 1px solid #edf1f6;
    //border-right: 1px solid #edf1f6;
    padding-left: 24px;
    padding-right: 24px;
    height: 60px;
    color: #242934;

    &.th {
      background: rgb(249, 250, 253);
      color: #646b7a;
    }
  }
}
</style>
