<template>
  <div class="content-bg">
    <div class="content">
      <div class="table-list">
        <button @click="openAddUser" class="table-list_buton">Добавить</button>
        <table class="iksweb">
          <thead>
            <tr>
              <th>Имя</th>
              <th>Телефон</th>
            </tr>
          </thead>
          <TableUserItem :model="allUsers" :usersClone="usersClone" />
        </table>
      </div>
      <div class="form-add" v-if="visibleAddUser">
        <AddUserForm
          :closeAddUser="closeAddUser"
          :allUsers="allUsers"
          ref="childComponent"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AddUserForm from "./AddUserForm.vue";
import TableUserItem from "./TableUserItem.vue";
export default {
    components: {
        AddUserForm,
        TableUserItem,
    },
    name: "HelloWorld",
    data() {
        return {
        visibleAddUser: false,
        allUsers: {
            name: "My Tree_1",
            children: [
            {
                name: "hello_2",
                children: [],
            },
            {
                name: "wat_3",
                children: [],
            },
            {
                name: "child folder_4",
                children: [
                {
                    name: "child folder_5",
                    children: [
                    {
                        name: "hello_6",
                        children: [
                        {
                            name: "hello_7",
                            children: [],
                        },
                        {
                            name: "wat_8",
                            children: [],
                        },
                        ],
                    },
                    {
                        name: "wat_9",
                        children: [],
                    },
                    ],
                },
                {
                    name: "hello_10",
                    children: [],
                },
                {
                    name: "wat_11",
                    children: [],
                },
                {
                    name: "child folder_12",
                    children: [
                    {
                        name: "hello_13",
                        children: [],
                    },
                    {
                        name: "wat_14",
                        children: [],
                    },
                    ],
                },
                ],
            },
            ],
        },
        };
    },
    methods: {
        closeAddUser() {
            this.visibleAddUser = false;
        },
        openAddUser() {
            return new Promise((resolve) => {
                this.visibleAddUser = true;
                setTimeout(() => {
                    this.addOptionsToSelect(this.allUsers);
                    resolve();
                }, 500);
            });
        },
        addOptionsToSelect(node) {
            var option = document.createElement("option");
            option.text = node.name;
            option.value = node.name;
            const childElement = this.$refs.childComponent.$refs.childSelect;
            childElement.add(option);
            if (node.children) {
                for (var i = 0; i < node.children.length; i++) {
                    this.addOptionsToSelect(node.children[i]);
                }
            }
        },
    },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
table.iksweb {
  border-collapse: collapse;
  border-spacing: 0;
  height: auto;
}
table.iksweb,
table.iksweb td,
table.iksweb th {
  border: 1px solid #595959;
  background-color: #fff;
}
table.iksweb td,
table.iksweb th {
  padding: 3px;
  width: 30px;
  height: 35px;
}
.content {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  width: 80%;
  margin: 0 auto;
  padding-top: 50px;
}
.content-bg {
  background: url("../assets/list.jpg");
  width: 100vw;
  height: 100vh;
}
.form-add {
  background-color: #fff;
  border: 1px solid #000;
  padding: 15px;
}
.table-list_buton {
  background-color: #e0e0e0;
  color: #000;
  border: 1px solid #000;
  padding: 8px 30px;
  border-radius: 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>