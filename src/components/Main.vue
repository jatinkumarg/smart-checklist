<template>
  <div>
    <form id="shopping-list">
      <h2>Welcome to Smart Checklist 👋</h2>
      <br />
      <br />
      <br />
      <div class="container">
        <div class="row">
          <div class="col-sm-4">
            <h4>New Product</h4>
            <br />
            Product
            <input
              type="text"
              v-model="itemName"
              class="checkbox ml-2"
              placeholder="Product name"
            />
            <br />
            <br />
            Quantity
            <input
              type="number"
              v-model="quantity"
              class="checkbox"
              placeholder="0"
              autofocus
            />
            <br />
            <br />
            <span
              v-if="itemNameMessage.length != 0"
              style="color:red;"
              class="ml-2"
            >
              {{ itemNameMessage }}
              <br />
              <br />
            </span>
            <button type="button" @click="addItem()" class="btn btn-primary">
              <i class="fa fa-plus"></i> Add Product
            </button>
          </div>
          <div class="col-sm-8">
            <table
              id="shopping-list-table"
              class="table table-condensed table-hover"
            >
              <thead>
                <tr>
                  <th>Product</th>
                  <th>Quantity</th>
                  <th>Actions</th>
                </tr>
              </thead>
              <tr v-bind:key="index" v-for="(item, index) in itemsList">
                <td>
                  <span v-show="!item.inEditMode">{{ item.itemName }}</span>
                  <input
                    v-bind:placeholder="item.itemName"
                    v-show="item.inEditMode"
                    v-model="item.itemName"
                  />
                </td>
                <td>
                  <span v-show="!item.inEditMode">{{ item.quantity }}</span>
                  <input
                    type="number"
                    v-bind:placeholder="item.quantity"
                    v-show="item.inEditMode"
                    v-model="item.quantity"
                  />
                </td>
                <td>
                  <button
                    type="button"
                    class="btn btn-success"
                    v-show="item.inEditMode"
                    @click="editItemComplete(item)"
                  >
                    <i class="fa fa-save"></i> Save
                  </button>
                  <button
                    type="button"
                    class="btn btn-info"
                    v-show="!item.inEditMode"
                    @click="editItem(item)"
                  >
                    <i class="fa fa-edit"></i> Edit
                  </button>
                  <button
                    type="button"
                    class="btn btn-danger"
                    @click="removeItem(index)"
                  >
                    <i class="fa fa-remove"></i> Delete
                  </button>
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "Main",
  data: function() {
    return {
      quantity: 0,
      itemName: "",
      itemsList: [
        {
          quantity: 12,
          itemName: "Apples",
          inEditMode: false
        },
        {
          quantity: 6,
          itemName: "Bananas",
          inEditMode: false
        }
      ],
      inEditMode: false,
      itemNameMessage: ""
    };
  },
  methods: {
    addItem: function() {
      let qty = this.quantity;
      let item = this.itemName.trim();

      if (this.itemName.trim()) {
        this.itemsList.push({
          quantity: qty,
          itemName: item,
          inEditMode: false
        });
        this.clearAll();
      } else {
        this.itemNameMessage = "Please provide product name";
      }
    },
    clearAll: function() {
      this.quantity = 0;
      this.itemName = "";
      this.itemNameMessage = "";
    },
    removeItem: function(index) {
      this.itemsList.splice(index, 1);
    },
    editItem: function(item) {
      item.inEditMode = true;
    },
    editItemComplete: function(item) {
      item.inEditMode = false;
    }
  }
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
body {
  padding: 1%;
  background-color: #abca;
}

h2,
h4 {
  font-family: "Nunito", sans-serif;
}

#shopping-list-table {
  table-layout: fixed;
  vertical-align: middle;
}

button {
  margin-left: 2%;
}
</style>
