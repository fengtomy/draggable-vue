<template>
    <div class="draggable" ref="draggable">
        <div
            class="label"
            v-for="label in list"
            :key="label.id"
            :draggable-id="label.id"
            :draggable="true"
            @dragstart="dragstart"
            @dragover="dragover"
            @drop="drop"
        >
            <slot name="draggableItem" :label="label"></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: "draggable",
        props: {
            list: {
                type: Array,
                required: true
            },
            // insert mode: insert after drop item
            // exchange mode: exchange the positions of drag and drop items
            insertType: {
                type: String,
                default: "insert"
            }
        },
        data() {
            return {
                dragItem: null,
                dropItem: null
            };
        },
        methods: {
            dragstart($e) {
                const id = $e.target.getAttribute("draggable-id");
                const item = this.list.filter(label => label.id + "" === id)[0];
                if (item) {
                    this.dragItem = item;
                }
            },
            dragover($e) {
                $e.preventDefault();
            },
            fixDropItem(node) {
                const name = node.getAttribute("draggable-id");
                if (node !== document.body && name) {
                    return name;
                }
                return this.fixDropItem(node.parentNode);
            },
            drop($e) {
                const { list, insertType } = this;
                const id = this.fixDropItem($e.target);
                const item = list.filter(label => label.id + "" === id)[0];
                if (item) {
                    this.dropItem = item;
                }
                if (this.dragItem && this.dropItem && this.dragItem !== this.dropItem) {
                    const dragIndex = list.indexOf(this.dragItem),
                        dropIndex = list.indexOf(this.dropItem);
                    if (~dragIndex && ~dropIndex) {
                        if (insertType === "insert") {
                            if (dropIndex > dragIndex) {
                                list.splice(dropIndex + 1, 0, this.dragItem);
                                list.splice(dragIndex, 1);
                            } else {
                                list.splice(dragIndex, 1);
                                list.splice(dropIndex + 1, 0, this.dragItem);
                            }
                        }
                        if (insertType === "exchange") {
                            list.splice(dropIndex, 1, this.dragItem);
                            list.splice(dragIndex, 1, this.dropItem);
                        }
                    }
                }
            }
        }
    }
</script>

<style scoped>
.draggable {
    width: 50%;
    height: 300px;
    margin: 100px auto;
    border: 1px solid #000;
    overflow-x: hidden;
    overflow-y: auto;
    border-radius: 2px;
}
    .label {
        display: inline-block;
        line-height: 28px;
        font-size: 14px;
        padding: 0 10px;
        margin: 5px 5px;
        border: 1px solid #ccc;
        border-radius: 4px;
        cursor: pointer;
    }
</style>