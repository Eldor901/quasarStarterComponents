<template>
  <q-page class="q-pa-sm">

    <div class="row q-col-gutter-sm q-py-sm">
      <div class="col-lg-12 col-md-12 col-sm-12 col-xs-12">
        <q-card class="text-grey-8">
          <q-card-section class="q-pa-none">
            <q-table class="no-shadow"
                     :data="data"
                     title="Page Visits"
                     :hide-header="mode === 'grid'"
                     :columns="columns"
                     row-key="name"
                     :filter="filter"
                     :pagination.sync="pagination"
            >
              <template v-slot:top-right="props">
                <q-input borderless dense debounce="300" v-model="filter" placeholder="Search">
                  <template v-slot:append>
                    <q-icon name="search"/>
                  </template>
                </q-input>

                <q-btn
                  flat
                  round
                  dense
                  :icon="props.inFullscreen ? 'fullscreen_exit' : 'fullscreen'"
                  @click="props.toggleFullscreen"
                  v-if="mode === 'list'" class="q-px-sm"
                >
                  <q-tooltip
                    :disable="$q.platform.is.mobile"
                    v-close-popup
                  >{{props.inFullscreen ? 'Exit Fullscreen' : 'Toggle Fullscreen'}}
                  </q-tooltip>
                </q-btn>

                <q-btn
                  color="primary"
                  icon-right="archive"
                  label="Export to csv"
                  no-caps
                  @click="exportTable"
                />
              </template>
            </q-table>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
    import IEcharts from 'vue-echarts-v3/src/full.js'
    import {exportFile} from 'quasar'


    export default {
        name: 'PageIndex',
        components: {
        },
        data() {
            return {
                filter: '',
                mode: 'list',
                columns: [
                    {name: 'id', align: 'left', label: 'User ID', field: 'id', sortable: true},
                    {name: 'user_name', align: 'left', label: 'User Name', field: 'user_name', sortable: true},
                    {
                        name: 'desc',
                        required: true,
                        label: 'Page',
                        align: 'left',
                        field: row => row.name,
                        sortable: true
                    },
                    {
                        name: 'date',
                        align: 'right',
                        label: 'Date',
                        field: 'date',
                        sortable: true
                    }
                ],
                data: [
                    {
                        id: "U0001",
                        name: '/login',
                        date: '12-10-2019',
                        user_name: 'Pratik Patel'
                    },
                    {
                        id: "U0002",
                        name: '/Dashboard',
                        date: '11-02-2019',
                        user_name: 'Razvan Stoenescu'
                    },
                    {
                        id: "U0003",
                        name: '/Map',
                        date: '03-25-2019',
                        user_name: 'Pratik Patel'
                    },
                    {
                        id: "U0004",
                        name: '/Mail',
                        date: '03-18-2019',
                        user_name: 'Jeff Galbraith'
                    },
                    {
                        id: "U0005",
                        name: '/Profile',
                        date: '04-09-2019',
                        user_name: 'Pratik Patel'
                    },
                ],
                pagination: {
                    rowsPerPage: 2
                },

            }
        },
        methods: {}
    }
</script>
