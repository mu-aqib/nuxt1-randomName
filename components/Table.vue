<script lang="ts" setup>
interface Name{
    generatedName: String[]    //Array of strings
}
    let props = defineProps<Name>()
</script>

<template>
    <table class="table">
        <thead>
            <th>S.No</th>
            <th>Name</th>
        </thead>
        <tbody>
            <tr v-for="(name, index) in generatedName" :key="index">
                <td data-label="S.No"> {{index}} </td>
                <td data-label="Name"> {{name}} </td>
            </tr>
        </tbody>
    </table>
</template>