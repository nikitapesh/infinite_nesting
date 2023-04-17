<template>
    <li>
        <div :class="{ bold: isFolder }" @click="toggle" @dblclick="changeType">
            {{ model.name }}
            <span v-if="isFolder">[{{ isOpen ? "-" : "+" }}]</span>
        </div>
        <ul v-show="isOpen" v-if="isFolder">
            <TableUserItem
                class="item"
                v-for="model in model.children"
                :key="model"
                :model="model"
            />
            <li class="add" @click="addChild">+</li>
        </ul>
    </li>
</template>

<script>
export default {
    props: ["model", "usersClone"],
    name: "TableUserItem",
    data() {
        return {
            isOpen: false,
        };
    },
    computed: {
        isFolder() {
            return this.model.children && this.model.children.length;
        },
    },
    methods: {
        toggle() {
            if (this.isFolder) {
                this.isOpen = !this.isOpen;
            }
        },
        changeType() {
            if (!this.isFolder) {
                this.model.children = [];
                this.addChild();
                this.isOpen = true;
            }
        },
        addChild() {
            this.model.children.push({
                name: "new stuff",
            });
        },
    },
};
</script>

<style>
</style>