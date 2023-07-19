<template>
  <div class="game">
    <div class="board">
      <div class="row" v-for="(row, rowIndex) in board" :key="rowIndex">
        <div class="cell" v-for="(cell, colIndex) in row" :key="colIndex"
          :class="{ selected: cell.selected, matched: cell.matched }" @click="handleCellClick(rowIndex, colIndex)">
          {{ cell.value }}
        </div>
      </div>
    </div>
    <div class="score">Score: {{ score }}</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      board: [],
      selectedCells: [],
      score: 0
    };
  },
  mounted() {
    this.generateBoard();
  },
  methods: {
    generateBoard() {
      this.board = [];
      const numbers = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5];
      numbers.sort(() => Math.random() - 0.5);
      const numRows = 6; // 游戏板的行数
      const numCols = 3; // 游戏板的列数
      for (let i = 0; i < numRows; i++) {
        let row = [];
        for (let j = 0; j < numCols; j++) {
          if (i < 6 && j < 6) {
            // 前6行前6列使用随机数生成格子的值
            const randomNumber = Math.floor(Math.random() * 10)
            row.push(
              { value: numbers[randomNumber], selected: false, matched: false },
              { value: numbers[randomNumber], selected: false, matched: false }
            );
          } else {
            // 其他格子的值设为0，表示它们不参与游戏
            row.push({ value: 0, selected: false, matched: false });
          }
        }
        row.sort(() => Math.random() - 0.5);
        this.board.push(row);
      }
    },
    handleCellClick(row, col) {
      // 如果点击的格子已经被标记为匹配状态，则直接返回
      if (this.board[row][col].matched) {
        return;
      }
      // 如果当前已选中了两个格子，则取消之前的选中状态
      if (this.selectedCells.length === 2) {
        this.selectedCells.forEach((cell) => {
          this.board[cell.row][cell.col].selected = false;
        });
        this.selectedCells = [];
      }
      // 将当前格子标记为选中状态，并将其添加到已选中格子的数组中
      this.board[row][col].selected = true;
      this.selectedCells.push({ row, col });
      // 如果已选中两个格子，则判断它们的值是否相等
      if (this.selectedCells.length === 2) {
        const cell1 = this.selectedCells[0];
        const cell2 = this.selectedCells[1];
        if (this.board[cell1.row][cell1.col].value === this.board[cell2.row][cell2.col].value) {
          // 如果两个格子的值相等，则将它们标记为匹配状态，并更新得分
          this.board[cell1.row][cell1.col].matched = true;
          this.board[cell2.row][cell2.col].matched = true;
          this.score += 10;
          // 延迟一段时间后，移除匹配状态的格子，并重新渲染游戏板
          setTimeout(() => {
            this.removeMatchedCells();
          }, 500);
        } else {
          // 如果两个格子的值不相等，则延迟一段时间后，取消它们的选中状态，并重新渲染游戏板
          setTimeout(() => {
            this.selectedCells.forEach((cell) => {
              this.board[cell.row][cell.col].selected = false;
            });
            this.selectedCells = [];
            this.render();
          }, 500);
        }
      } else {
        // 如果当前只选中了一个格子，则直接重新渲染游戏板
        this.render();
      }
    },
    removeMatchedCells() {
      // 遍历所有格子，将标记为匹配状态的格子从游戏板中移除
      for (let i = 0; i < this.board.length; i++) {
        for (let j = 0; j < this.board[i].length; j++) {
          if (this.board[i][j].matched) {
            // 将标记为匹配状态的格子从游戏板中移除，并将其值设为0
            this.board[i][j].value = 0;
          }
        }
      }
      // 更新得分
      this.score += 10;
      // 延迟一段时间后，重新渲染游戏板
      setTimeout(() => {
        this.render();
      }, 500);
    },
    render() {
      this.$forceUpdate();
    }
  }
};
</script>

<style scoped>
.game {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

.board {
  display: flex;
  flex-wrap: wrap;
  width: 288px;
  height: 288px;
  border: 0.5px solid #e5e7eb;
  border-radius: 5px;
  padding: 5px;
}

.row {
  display: flex;
  flex-basis: 20%;
}

.cell {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
  margin: 2px;
  font-size: 20px;
  font-weight: bold;
  background-color: #fff;
  border: 2px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
}

.selected {
  background-color: #ff0;
}

.matched {
  background-color: green;
}

.score {
  margin-top: 20px;
  font-size: 24px;
  font-weight: bold;
}
</style>