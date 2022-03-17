<template>
  <v-data-table :sort="sort" @sorted="onSort" :values="value" :columns="columns" :loading="false" >
    <template #column_color="prop">
      <color :person="prop.value" />
    </template>
  </v-data-table>
</template>

<script lang="ts">
import {Options, Vue} from 'vue-class-component';
import VDataTable from "@/components/VDataTable.vue";
import {ColumnData} from "@/components/VDataTable.vue";
import Color from "@/components/Color.vue";
import {Watch} from "vue-property-decorator";

@Options({
  components: {
    VDataTable,
    Color
  },
})
export default class Home extends Vue {
  columns: ColumnData[] = [
    {
      sortable: true,
      sort: '',
      name: 'user',
      class: '',
      default: '-',
      label: 'User'
    },
    {
      sortable: true,
      sort: '',
      name: 'role',
      class: '',
      default: '-',
      label: 'Role'
    },
    {
      sortable: false,
      sort: '',
      name: 'color',
      class: '',
      default: '',
      label: 'Color'
    }
  ];

  value: any[] = [
    {
      user: 'Daniel',
      role: 'Dev',
      color: 'red'
    },
    {
      user: 'Federico',
      role: 'Dev',
      color: 'rebeccapurple'
    },
    {
      user: 'Bea',
      role: 'designer',
      color: 'gray'
    },
    {
      user: 'Gabbo',
      role: 'Sales',
      color: 'green'
    }
  ];

  sort = '';

  onSort(value: string) {
    this.sort = value;
  }

  @Watch('sort')
  onSortChange() {
    if(this.sort[0] === '-') {
      const s = this.sort.slice(1);
      this.value.sort((a: any, b: any) => {
        if(a[s].toLowerCase() < b[s].toLowerCase()) {
          return 1;
        }
        if(a[s].toLowerCase() > b[s].toLowerCase()) {
          return -1
        }
        return 0;
      });
    } else {
      this.value.sort((a: any, b: any) => {
        if(a[this.sort].toLowerCase() < b[this.sort].toLowerCase()) {
          return -1;
        }
        if(a[this.sort].toLowerCase() > b[this.sort].toLowerCase()) {
          return 1;
        }
        return 0;
      });
    }
  }
}
</script>
