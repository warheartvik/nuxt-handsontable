<template>
    <hot-table
    key="non-commercial-and-evaluation"
    :data="data"
    :settings="hotSettings"></hot-table>
</template>
<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
//@ts-ignore
import HotTable from "~/plugins/vue-handsontable";
import Handsontable from "handsontable";

@Component({
  components: {
    HotTable
  }
})
export default class comHandsOnTable extends Vue {
    data: object = [
        [10, true, 12, 13], 
        [20, true, 14, 13], 
        [30, false, 12, 13]
    ];
    marcas: any = ["Ford", "Volvo", "Toyota", "Honda"]
    hotSettings: {} = {
        licenseKey: "non-commercial-and-evaluation",
        colHeaders: ["Ford", "Volvo", "Toyota", "Honda"],
        rowHeaders: ["2016", "2017", "2018"],
        stretchH: "all",
        columns: [
            { type: 'numeric'},
            { type: 'checkbox'},
            { type: 'dropdown', source: this.marcas },
            { type: 'date'}
        ],
        afterChange: (changes) => {
            console.log(changes)
            //@ts-ignore
            // let fila = this.getData()[changes[0]];
            // changes.forEach(([row, prop, oldValue, newValue]) => {
            // // Some logic...
            // });
        },
        contextMenu: {
            items: {
                row_above: {
                name: "Insert row above this one (custom name)"
                },
                row_below: {},
                //@ts-ignore
                separator: Handsontable.plugins.ContextMenu.SEPARATOR,
                clear_custom: {
                name: "Clear all cells (custom)",
                    callback: function() {
                        //@ts-ignore
                        this.clear();
                    }
                }
            }
        }
    };
    afterSelection(event) {
        console.log(event);
    }
    afterChange(event){
        console.log(event);
    }
}
</script>

<style src="~/node_modules/handsontable/dist/handsontable.full.css"></style>