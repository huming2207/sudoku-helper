<template>
  <div class="sudoku">
    <b-container class="mt-5">
      <b-card>
        <table>
          <tr v-for="(row, rowIdx) in items" :key="row">
            <td v-for="(col, colIdx) in row" :key="col">
              <input :id="rowIdx.toString() + '-' + col.toString()"  max="5" style="width:15%" v-model.number="items[rowIdx][colIdx]" type="number">
            </td>
          </tr>
        </table>
      </b-card>
      <b-card>
        <div>
          Enter size: <input type="number" style="width:15%" v-model.number="size">
        </div>
      </b-card>
      <b-card>
        <div>
          Min value: <input type="number" style="width:15%" v-model.number="minVal">
        </div>
      </b-card>
      <b-card>
        <div>
          Max value: <input type="number" style="width:15%" v-model.number="maxVal">
        </div>
      </b-card>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'Sudoku',
  data: function () {
    return {
      items: [[1, 2, 3], [4, 5, 6], [7, 8, 9]],
      size: 3,
      minVal: 0,
      maxVal: 1,
    }
  },
  methods: {
    calculate() {
      for(let row = 0; row < this.items.size; row += 1) {
        for(let col = 0; col < this.items.size; col += 1) {
          // items[row][col]
        }
      }
    }
  }
}
</script>