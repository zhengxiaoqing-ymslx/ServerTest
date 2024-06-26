<script setup>
  import {
    useI18n
  } from 'vue-i18n';
  import {
    useApi
  } from '@/composables/useApi';
  const {
    t
  } = useI18n();
  const currentValue = ref();
  defineOptions({
    name: 'tree',
  });
  const form = ref();
  const viy2Row_qAo0y = ref();
  const department = ref();
  const viy2Tree_quwFz = ref();
  const details = ref();
  const viy2Table_qFvXH = ref();
  const formData = reactive({});
  const viy2Table_qFvXHEditConfig = reactive({
    trigger: 'click'
  });
  const detailDsApi = useApi({
    method: 'post',
    localData: [{
      "mail": "john.doe@ymsl.com.cn",
      "name": "Accounting",
      "id": "1",
      "dept": "AD"
    }, {
      "mail": "emily.smith@ymsl.com.cn",
      "name": "Cost Control",
      "id": "2",
      "dept": "CCD"
    }, {
      "mail": "sarah.wilson@ymsl.com.cn",
      "name": "Tax",
      "id": "3",
      "dept": "TD"
    }, {
      "mail": "jessica.taylor@ymsl.com.cn",
      "name": "Sales Operations",
      "id": "4",
      "dept": "SOD"
    }, {
      "mail": "william.jackson@ymsl.com.cn",
      "name": "Channel Sales",
      "id": "5",
      "dept": "CSD"
    }, {
      "mail": "olivia.white@ymsl.com.cn",
      "name": "Sales Support",
      "id": "6",
      "dept": "SSD"
    }, {
      "mail": "james.martin@ymsl.com.cn",
      "name": "Market Research",
      "id": "7",
      "dept": "MRD"
    }, {
      "mail": "sophia.moore@ymsl.com.cn",
      "name": "Brand Management",
      "id": "8",
      "dept": "BMD"
    }, {
      "mail": "benjamin.harris@ymsl.com.cn",
      "name": "Digital Marketing",
      "id": "9",
      "dept": "DMD"
    }, {
      "mail": "ava.clark@ymsl.com.cn",
      "name": "Accounting",
      "id": "10",
      "dept": "AD"
    }, {
      "mail": "jacob.lewis@ymsl.com.cn",
      "name": "Accounting",
      "id": "11",
      "dept": "AD"
    }, {
      "mail": "mia.robinson@ymsl.com.cn",
      "name": "Cost Control",
      "id": "12",
      "dept": "CCD"
    }, {
      "mail": "ethan.walker@ymsl.com.cn",
      "name": "Tax",
      "id": "13",
      "dept": "TD"
    }, {
      "mail": "chloe.hall@ymsl.com.cn",
      "name": "Sales Operations",
      "id": "14",
      "dept": "SOD"
    }, {
      "mail": "emma.hill@ymsl.com.cn",
      "name": "Channel Sales",
      "id": "15",
      "dept": "CSD"
    }, ],
  }, {
    onSuccess: (data, params) => {
      if (currentValue.value && currentValue.value !== 'Yamaha') {
        detailDs.value = data.filter((item) => {
          return item.dept === currentValue.value;
        })
      }
    },
  });
  const detailDs = detailDsApi.data;
  const treeDsApi = useApi({
    method: 'post',
    localData: [{
      "children": [{
        "children": [{
          "children": [],
          "id": "3",
          "label": "CCD",
          "value": "CCD"
        }, {
          "children": [],
          "id": "4",
          "label": "TD",
          "value": "TD"
        }],
        "id": "2",
        "label": "AD",
        "value": "AD"
      }, {
        "children": [{
          "children": [],
          "id": "6",
          "label": "CSD",
          "value": "CSD"
        }, {
          "children": [],
          "id": "7",
          "label": "SSD",
          "value": "SSD"
        }],
        "id": "5",
        "label": "SOD",
        "value": "SOD"
      }, {
        "children": [{
          "children": [],
          "id": "9",
          "label": "BMD",
          "value": "BMD"
        }, {
          "children": [],
          "id": "10",
          "label": "DMD",
          "value": "DMD"
        }],
        "id": "8",
        "label": "MRD",
        "value": "MRD"
      }],
      "id": "1",
      "label": "Yamaha Information",
      "value": "Yamaha"
    }],
  });
  const treeDs = treeDsApi.data;
  const viy2Tree_quwFzNodeClick = (data, node, e) => {
    currentValue.value = data.value;
    detailDsApi.runAsync();
  };
  const viy2Tree_quwFz_input = ref();
  const viy2Tree_quwFz_flex = ref();
  const viy2Tree_quwFzProps = reactive({
    value: 'id',
    label: 'label',
    children: 'children',
    disabled: 'disabled'
  });
  const viy2Table_qFvXHIdEditRender = computed(() => {
    return {
      enabled: false,
    };
  });
  const viy2Table_qFvXHNameEditRender = computed(() => {
    return {
      enabled: false,
    };
  });
  const viy2Table_qFvXHDeptEditRender = computed(() => {
    return {
      enabled: false,
    };
  });
  const viy2Table_qFvXHMailEditRender = computed(() => {
    return {
      enabled: false,
    };
  });
</script>
<template>
  <VueForm ref="form" :model="formData">
    <VueRow id="viy2Row_qAo0y" ref="viy2Row_qAo0y">
      <VueCol item-key="item" :md="{span:6}">
        <VuePanel title="Department" :collapse="true" id="department" ref="department">
          <VueTree :default-expand-all="true" height="300px" id="viy2Tree_quwFz" ref="viy2Tree_quwFz" @node-click="viy2Tree_quwFzNodeClick" :data="treeDs" :props="viy2Tree_quwFzProps">
          </VueTree>
        </VuePanel>
      </VueCol>
      <VueCol item-key="item" class="detailCls" :md="{span:18}">
        <VuePanel title="Details Department" id="details" ref="details">
          <VueTable :stripe="true" :border="true" height="710px" id="viy2Table_qFvXH" ref="viy2Table_qFvXH" :data="detailDs" :edit-config="viy2Table_qFvXHEditConfig">
            <VueInputColumn :edit-render="viy2Table_qFvXHIdEditRender" field="id" title="no" width="150px">
            </VueInputColumn>
            <VueInputColumn :edit-render="viy2Table_qFvXHNameEditRender" field="name" title="name" width="200px">
            </VueInputColumn>
            <VueInputColumn :edit-render="viy2Table_qFvXHDeptEditRender" field="dept" title="department" width="200px">
            </VueInputColumn>
            <VueInputColumn :edit-render="viy2Table_qFvXHMailEditRender" field="mail" title="mail" min-width="250px">
            </VueInputColumn>
          </VueTable>
        </VuePanel>
      </VueCol>
    </VueRow>
  </VueForm>
</template>
<style type="text/css" scoped>
  .detailCls {
    padding-left: 6px;
  }
</style>