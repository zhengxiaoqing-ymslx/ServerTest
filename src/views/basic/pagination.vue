<script setup>
  import {
    IconSearch,
  } from 'viy-ui';
  import {
    useI18n
  } from 'vue-i18n';
  import {
    useApi
  } from '@/composables/useApi';
  const {
    t
  } = useI18n();
  defineOptions({
    name: 'pagination',
  });
  const form = ref();
  const viy2Panel_KFRLT = ref();
  const viy2Row_PwIOB = ref();
  const searchBtn = ref();
  const viy2Table_KGt5s = ref();
  const pagination = ref();
  const formData = reactive({});
  const viy2Table_KGt5sEditConfig = reactive({});
  const paginationCurrentPage = ref(1);
  const paginationPageSize = ref(10)
  const employeeListApi = useApi({
    url: '/employee/getEmployeeMstListPageable',
    method: 'post',
    data: () => {
      formData.pageSize = paginationPageSize.value;
      formData.currentPage = paginationCurrentPage.value;
      return formData;
    },
  }, {
    initialData: {
      data: []
    },
  });
  const employeeList = employeeListApi.data;
  const searchBtnClick = () => {
    employeeListApi.runAsync();
  };
  const viy2Table_KGt5sEmployeeCdEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'left',
      },
    };
  });
  const viy2Table_KGt5sEmployeeNmEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'left',
      },
    };
  });
  const viy2Table_KGt5sGroupNmEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'left',
      },
    };
  });
  const viy2Table_KGt5sJoinDateEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'center',
        type: 'dates',
      },
    };
  });
  const viy2Table_KGt5sGenderFormatter = function(row, columnConfig, cellValue) {
    if (row.cellValue == '0') {
      return row.cellValue = 'male';
    }
    if (row.cellValue == '1') {
      return row.cellValue = 'female';
    }
  };
  const viy2Table_KGt5sGenderEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'center',
      },
    };
  });
  const viy2Table_KGt5sMailAddressEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'left',
      },
    };
  });
  const paginationCurrentChange = // When flipping pages, retrieve data based on page and size
    () => {
      employeeListApi.runAsync();
    };
</script>
<template>
  <VueForm ref="form" :model="formData">
    <VuePanel :title="t('detailsArea')" id="viy2Panel_KFRLT" ref="viy2Panel_KFRLT"> <template #header>
        <div style="width: 300px">
          <VueRow id="viy2Row_PwIOB" ref="viy2Row_PwIOB">
            <VueCol item-key="item" align="right" :inline="true" :md="{span:24}">
              <VueButton type="primary" id="searchBtn" ref="searchBtn" @click="searchBtnClick" :icon="IconSearch">
                {{t('search')}}
              </VueButton>
            </VueCol>
          </VueRow>
        </div>
      </template>
      <VueTable height="700px" id="viy2Table_KGt5s" ref="viy2Table_KGt5s" :data="employeeList.content" :edit-config="viy2Table_KGt5sEditConfig">
        <VueInputColumn :edit-render="viy2Table_KGt5sEmployeeNmEditRender" field="employeeNm" align="left" width="200px" :title="t('employeeNm')" header-align="center">
        </VueInputColumn>
        <VueInputColumn :edit-render="viy2Table_KGt5sGroupNmEditRender" field="groupNm" align="left" width="200px" :title="t('groupNm')" header-align="center">
        </VueInputColumn>
        <VueDateTimeColumn :edit-render="viy2Table_KGt5sJoinDateEditRender" field="joinDate" align="center" width="200px" :title="t('joinDate')" header-align="center">
        </VueDateTimeColumn>
        <VueInputColumn :formatter="viy2Table_KGt5sGenderFormatter" :edit-render="viy2Table_KGt5sGenderEditRender" field="gender" align="center" width="200px" :title="t('gender')" header-align="center">
        </VueInputColumn>
        <VueInputColumn :edit-render="viy2Table_KGt5sMailAddressEditRender" field="mailAddress" align="left" width="200px" :title="t('mailAddress')" header-align="center">
        </VueInputColumn>
      </VueTable>
    </VuePanel>
    <VuePagination layout="total, sizes, prev, pager, next, jumper" id="pagination" ref="pagination" @current-change="paginationCurrentChange" v-model:current-page="paginationCurrentPage" v-model:page-size="paginationPageSize" :total="employeeList.totalElements || 0">
    </VuePagination>
  </VueForm>
</template>