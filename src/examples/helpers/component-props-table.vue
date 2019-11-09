<template>
    <div>
        <table class="app-table">
            <thead>
                <tr>
                    <th style="min-width:119.68px;">Name</th>
                    <th>Type</th>
                    <th>Required</th>
                    <th>Description</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(property,index) in properties"
                    :key="index">
                    <td>{{property.name}}</td>
                    <td>{{property.type}}</td>
                    <td>{{property.required}}</td>
                    <td>{{property.description}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        props: {
            properties: Array,
        },
    }
</script>

<style>
    @import './app-table-styles.css';
</style>  