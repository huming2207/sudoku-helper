<template>
  <div class="sudoku">
    <b-container class="mt-5">
      <b-card>
        <table>
          <tr v-for="(row, rowIdx) in items" :key="row">
            <td v-for="(col, colIdx) in row" :key="col">
              <input :id="rowIdx.toString() + '-' + col.toString()"  max="5" style="width:15%" v-model="items[rowIdx][colIdx]">
            </td>
          </tr>
        </table>
      </b-card>
      <b-card>
          Enter size: <input type="number" style="width:15%" v-model.number="size">
      </b-card>
      <b-card>
          Min value: <input type="number" style="width:15%" v-model.number="minVal">
      </b-card>
      <b-card>
          Max value: <input type="number" style="width:15%" v-model.number="maxVal">
      </b-card>
      <b-card>
        <b-button variant="success" v-on:click="result = calculate()">Calculate</b-button>
      </b-card>
      <b-card>
          Result: x={{result}}
      </b-card>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'Sudoku',
  data: function () {
    return {
      items: [["1", "2", ""], ["", "x", ""], ["", "", ""]],
      size: 3,
      minVal: 0,
      maxVal: 1,
      possibleNum: ["1", "2", "3"],
      result: "(Unknown)"
    }
  },
  methods: {
    findX() {
      for(let row = 0; row < this.items.length; row += 1) {
        for(let col = 0; col < this.items.length; col += 1) {
          if(this.items[row][col] === "x") return { 'row': row, 'col': col }; // Maybe not only "x"??
        }
      }

      return { 'row': null, 'col': null };
    },

    addToSet() {
      const plHolder = this.findX();
      const boardSize = this.items.size;
      let numSet = new Set();
      
      // Vertical position (Iterate rows)
      for(let idx = 0; idx < boardSize; idx += 1) {
        const currItem = this.items[idx][plHolder.col];
        if(currItem && numSet.has(currItem) && currItem !== "x") numSet.add(currItem);
      }

      // Horizontal position (Iterate columns)
      for(let idx = 0; idx < boardSize; idx += 1) {
        const currItem = this.items[plHolder.row][idx];
        if(currItem && numSet.has(currItem) && currItem !== "x") numSet.add(currItem);
      }

      // Forward-slash/Up position (row+, col-)
      for(let rowIdx = plHolder.row, colIdx = plHolder.col; rowIdx < boardSize && colIdx >= 0; rowIdx += 1, colIdx -= 1) {
        const currItem = this.items[rowIdx][colIdx];
        if(currItem && numSet.has(currItem) && currItem !== "x") numSet.add(currItem);
      }

      // Forward-slash/Down position (row-, col+)
      for(let rowIdx = plHolder.row, colIdx = plHolder.col; colIdx < boardSize && rowIdx >= 0; colIdx += 1, rowIdx -= 1) {
        const currItem = this.items[rowIdx][colIdx];
        if(currItem && numSet.has(currItem) && currItem !== "x") numSet.add(currItem);
      }

      // Backslash/Down position (row-, col-)
      for(let rowIdx = plHolder.row, colIdx = plHolder.col; colIdx < boardSize && rowIdx < boardSize; colIdx += 1, rowIdx += 1) {
        const currItem = this.items[rowIdx][colIdx];
        if(currItem && numSet.has(currItem) && currItem !== "x") numSet.add(currItem);
      }

      // Backslash/Down position (row+, col+)
      for(let rowIdx = plHolder.row, colIdx = plHolder.col; colIdx >= 0 && rowIdx >= 0; colIdx -= 1, rowIdx -= 1) {
        const currItem = this.items[rowIdx][colIdx];
        if(currItem && numSet.has(currItem) && currItem !== "x") numSet.add(currItem);
      }

      /* eslint-disable no-console */
      console.log(numSet);
      return numSet;
    },

    calculate() {
      const numSet = this.addToSet();
      for(const num of this.possibleNum) {
        if(!numSet.has(num)) return num;
      }

      /* eslint-disable no-console */
      console.error('Not possible??');
      return "(No Possible Answer)";
    }
  }
}
</script>