<template>
    <div id="app">
        <draggable :list="dataStore" :insert-type="type">
            <span slot="draggableItem" slot-scope="item" >
                {{ item.label.text }}
            </span>
        </draggable>
    </div>
</template>

<script>
    import Draggable from "./components/draggable";
    export default {
        name: 'app',
        components: {
            Draggable
        },
        data() {
            return {
                dataStore: [
                    { text: "name", id: 1 },
                    { text: "label", id: 2 },
                    { text: "war", id: 3 },
                    { text: "lol", id: 4 },
                    { text: "game", id: 5 },
                    { text: "basketball", id: 6 },
                    { text: "football", id: 7 },
                    { text: "run", id: 8 },
                    { text: "skip", id: 9 },
                    { text: "foot", id: 10 },
                    { text: "tail", id: 11 },
                    { text: "shallow", id: 12 },
                    { text: "border", id: 13 },
                    { text: "style", id: 14 },
                    { text: "font", id: 15 },
                    { text: "font-size", id: 16 },
                    { text: "font-family", id: 17 },
                    { text: "font-weight", id: 18 },
                    { text: "click", id: 19 },
                    { text: "input", id: 20 },
                    { text: "mouse", id: 21 },
                    { text: "cat", id: 22 },
                    { text: "banana", id: 23 },
                    { text: "pear", id: 24 }
                ],
                type: "exchange"
            };
        }
    }
</script>

<style>

</style>
