<template>
    <div class="row">

      <!-- STAFF -->
      <div class="col-12">
        <card class="card" :header-classes="{'text-right': isRTL}">
          <h4 slot="header" class="card-title">{{$t('dashboard.staff')}}</h4>
          <div class="table-responsive">
            <user-table></user-table>
          </div>
        </card>
      </div>

      <!-- PATIENTS -->
      <div class="col-12">
        <card class="card" :header-classes="{'text-right': isRTL}">
          <h4 slot="header" class="card-title">{{$t('dashboard.patients')}}</h4>
          <div class="table-responsive">
            <patient-table></patient-table>
          </div>
        </card>
      </div>
    </div>
</template>
<script>
import { BaseTable } from "@/components";
import UserTable from './Dashboard/UserTable';
import PatientTable from './Dashboard/PatientTable';
const tableColumns = ["Name", "Occupation", "DirectReport", "Code"];
const tableData = [
  {
    id: 1,
    name: "Dakota Rice",
    code: "$36.738",
    country: "Niger",
    city: "Oud-Turnhout",
  },
  {
    id: 2,
    name: "Minerva Hooper",
    code: "$23,789",
    country: "Curaçao",
    city: "Sinaai-Waas"
  },
  {
    id: 3,
    name: "Sage Rodriguez",
    code: "$56,142",
    country: "Netherlands",
    city: "Baileux"
  },
  {
    id: 4,
    name: "Philip Chaney",
    code: "$38,735",
    country: "Korea, South",
    city: "Overland Park"
  },
  {
    id: 5,
    name: "Doris Greene",
    code: "$63,542",
    country: "Malawi",
    city: "Feldkirchen in Kärnten"
  },
  {
    id: 6,
    name: 'Mason Porter',
    code: '$98,615',
    country: 'Chile',
    city: 'Gloucester'
  },
  {
    id: 7,
    name: 'Jon Porter',
    code: '$78,615',
    country: 'Portugal',
    city: 'Gloucester'
  }
];

export default {
  components: {
    BaseTable,
    UserTable,
    PatientTable
  },
  data() {
    return {
      table1: {
        title: "Current Staff on Shift",
        columns: [...tableColumns],
        data: [...tableData]
      },
      table2: {
        title: "Patients in Queue",
        columns: [...tableColumns],
        data: [...tableData]
      }
    };
  }
};
</script>
<style>
</style>
