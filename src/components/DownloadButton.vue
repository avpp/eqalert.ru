<template>
  <b-dropdown text="Выгрузить">
    <b-dropdown-item @click.prevent="download_xlsx"><i class="fa fa-fw fa-xs fa-file-excel-o" aria-hidden="true" /> XLSX</b-dropdown-item>
    <b-dropdown-item @click.prevent="download_csv"><i class="fa fa-fw fa-xs fa-file-zip-o" aria-hidden="true" /> CSV</b-dropdown-item>
  </b-dropdown>
</template>

<script>
import JsZip from 'jszip'
import XLSX from 'xlsx'
import saveAs from 'file-saver'

export default {
  props: {
    dataProvider: {
      type: Object,
      default: function() {
        return { getData: function() { return [] } }
      },
      validator: function(value) {
        return typeof ((value || {}).getData) === 'function'
      }
    },
    filename: {
      type: String,
      default: 'EqAlert_export_data'
    }
  },
  methods: {
    download_xlsx: function() {
      const data = this.dataProvider.getData()
      const wb = XLSX.utils.book_new()
      for (let s of data) {
        XLSX.utils.book_append_sheet(wb, XLSX.utils.aoa_to_sheet(s.content || []), s.name || '')
      }
      const result = XLSX.write(wb, {type: 'array', bookType: 'xlsx'})
      saveAs(new Blob([result], {type: 'application/octet-stream'}), this.filename + '.xlsx')
    },
    download_csv: function() {
      const data = this.dataProvider.getData()
      let zip = new JsZip()
      let idx = 1
      for (let s of data) {
        const val = XLSX.utils.sheet_to_csv(XLSX.utils.aoa_to_sheet(s.content || []))
        const name = 'sheet_' + idx + '_' + (s.name || '') + '.csv'
        zip.file(name, val)
      }
      zip.generateAsync({type: 'blob'}).then((blob) => {
        saveAs(blob, this.filename + '.zip')
      })
    }
  }
}
</script>
