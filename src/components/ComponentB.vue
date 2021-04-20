<template>
    <div>
        <p>{{ number }}</p>
        <button @click="handleUpdateNumber(number + 1, 'updated')">Increase</button>
        <button @click="handleIncrease">Increase</button>
    </div>
</template>

<script>
    export default {
        props: ['number', 'handleUpdateNumber'],
        methods: {
            handleIncrease() {
                const newValue = this.number + 1;
                this.handleUpdateNumber(newValue, 'updated');
                console.log(newValue,"ssss")
            }
        }
    }
</script>
