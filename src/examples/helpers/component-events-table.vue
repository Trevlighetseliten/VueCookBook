    <template>
    <div>
        <table class="app-table">
            <thead>
                <tr>
                    <th style="min-width:119.68px;">Event name</th>
                    <th>Args</th>
                    <th>Description</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(event, index) in events" 
                    :key="index">
                    <td>{{ event.name }}</td>
                    <td>{{ event.args }}</td>
                    <td>{{ event.description }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        props: {
            events: Array
        },
        
    }
</script>

<style>
    @import './app-table-styles.css';
</style>