<template>
  <div>
    <el-button type="primary" @click="submit()">提交</el-button>
    <br />
    <br />
    <fan-table row-key-field-name="rowKey" :fixed-header="true" :columns="columns" :table-data="tableData"
      :cell-selection-option="cellSelectionOption" :row-style-option="rowStyleOption" />
  </div>
</template>

<script lang="jsx">
export default {
  data() {
    return {
      rowStyleOption: {
        clickHighlight: false,
        hoverHighlight: false,
      },
      // submit data
      submitData: [
        // {
        //     rowKey: 0,
        //     field: "",
        //     value: "",
        // },
      ],
      cellSelectionOption: {
        // default true
        enable: false,
      },
      columns: [
        {
          field: '',
          key: 'a',
          title: '',
          width: 50,
          align: 'center',
          operationColumn: true,
          renderBodyCell: ({ row, column, rowIndex }, h) => {
            return ++rowIndex
          },
        },
        {
          field: 'name',
          key: 'name',
          title: 'Name',
          align: 'left',
          width: '15%',
        },
        {
          field: 'date',
          key: 'date',
          title: 'Date',
          align: 'left',
          width: '15%',
          renderBodyCell: ({ row, column, rowIndex }, h) => {
            return (
              <el-date-picker
                size="small"
                value={row.date}
                onInput={(val) => {
                  row.date = val
                  this.cellDataChange(row, column, val)
                }}
                type="date"
                value-format="yyyy-MM-dd"
                placeholder="选择日期"
              ></el-date-picker>
            )
          },
        },
        {
          field: 'age',
          key: 'age',
          title: 'Age',
          align: 'center',
          width: '30%',
          renderBodyCell: ({ row, column, rowIndex }, h) => {
            return (
              <el-input-number
                size="small"
                min={1}
                value={row.age}
                onInput={(val) => {
                  row.age = val
                }}
                onChange={(val) => {
                  this.cellDataChange(row, column, val)
                }}
              ></el-input-number>
            )
          },
        },
        {
          field: 'gender',
          key: 'gender',
          title: 'Gender',
          align: 'left',
          width: '40%',
          renderBodyCell: ({ row, column, rowIndex }, h) => {
            return (
              <el-select
                size="small"
                value={row.gender}
                onInput={(val) => {
                  row.gender = val
                  this.cellDataChange(row, column, val)
                }}
                placeholder="请选择"
              >
                <el-option label="female" value="female"></el-option>
                <el-option label="male" value="male"></el-option>
              </el-select>
            )
          },
        },
      ],
      // table data
      tableData: [
        {
          name: 'John',
          date: '1900-05-20',
          age: 17,
          gender: 'female',
          rowKey: 0,
        },
        {
          name: 'Dickerson',
          date: '1910-06-20',
          age: 20,
          gender: 'male',
          rowKey: 1,
        },
        {
          name: 'Larsen',
          date: '2000-07-20',
          age: 22,
          gender: 'female',
          rowKey: 2,
        },
        {
          name: 'Geneva',
          date: '2010-08-20',
          age: 18,
          gender: 'male',
          rowKey: 3,
        },
        {
          name: 'Jami',
          date: '2020-09-20',
          age: 29,
          gender: 'female',
          rowKey: 4,
        },
      ],
    }
  },
  methods: {
    // submit
    submit() {
      alert(JSON.stringify(this.submitData))
    },

    // cell data change
    cellDataChange(row, column, cellValue) {
      const { submitData } = this

      const currentCell = submitData.find(
        (x) => x.rowKey === row.rowKey && x.field === column.field,
      )

      if (currentCell) {
        currentCell.value = cellValue
      } else {
        const newCell = {
          rowKey: row.rowKey,
          field: column.field,
          value: cellValue,
        }
        this.submitData.push(newCell)
      }
    },
  },
}
</script>