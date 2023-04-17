<template>
  <div class="modal-bg">
    <div class="modal-content">
        <div class="modal-header">
            <h2>Добавление пользователя</h2>
            <p @click="closeAddUser" style="cursor:pointer;">&#10006;</p>
        </div>
        <form style="display: grid;">
            <label for="name">Имя</label>
            <input type="text" v-model="userName" name="name">
            <label for="userParent">Начальник</label>
            <select name="userParent" v-model="userParent" ref="childSelect">
                <option ref="childOption"></option>
            </select>
            <input type="button" value="Сохранить" @click="addUser(allUsers)">
        </form>
    </div>
  </div>
</template>

<script>
export default {
    props: ['closeAddUser', 'allUsers'],
    name: 'AddUserForm',
    data() {
        return {
            userName: null,
            userParent: null
        }
    },
    methods: {
        addUser(node) {
            if (node.children) {
                for (var i = 0; i < node.children.length; i++) {
                    if (node.children[i].name === this.userParent) {
                        node.children[i].children.push({
                            name: this.userName,
                            children: []
                        });
                        var option = document.createElement("option");
                        option.text = this.userName;
                        option.value = this.userName;
                        const childElement = this.$refs.childSelect;
                        childElement.add(option);
                        return true;
                    } else {
                        if (this.addUser(node.children[i])) {
                            return true;
                        }
                    }
                }
            }
            return false;
        }
    }
}
</script>

<style>
.modal-header{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>