<template>
    <div class="row">
        <div class="col-12 col-md-8">
            <p class="info-header">Description</p>
            <p class="info-text">A tab bar with customizable styling. Default styled tab bar used above. Custom styles can be added, which is explain under 'Usage'</p>
            <hr/>
        </div>
        <div class="col-12 col-md-8">
            <p class="info-header">Props</p>
            <component-props-table :properties="properties"></component-props-table>
            <hr/>
        </div>
        <div class="col-12 col-md-8">
            <p class="info-header">Events</p>
            <component-events-table :events="events"></component-events-table>
            <hr/>
        </div>
        <div class="col-12 col-md-8">
            <p class="info-header">Usage</p>
            <p class="info-text">A default styled tab bar, as the one used in this page, only requires tab information:</p>
            <pre class="horizontal-scroll"><code>{{defaultTabBarHtml}}</code></pre> 
            <p class="info-text">Custom styles can be added by providing class names as props to override the default looks of the tab bar. 
                The classes needs to be implemented with correct scope to affect the tab bar</p> 
            <pre><code>{{customCss}}</code></pre>
            <pre class="horizontal-scroll"><code>{{ customTabBarHtml }}</code></pre>
            <p class="info-text">The class styling must be implemented</p>
            <p class="info-text">which provides the following tab bar</p>
            <tab-panel :tabItems="tabs" :tabContainerClass="'my-tab-panel-container'" :tabItemClass="'my-tab-item'" @tabChanged="() => {}"></tab-panel>
        </div>
        

    </div>
</template>

<script>
    import ComponentPropsTable from './helpers/component-props-table.vue'
    import ComponentEventsTable from './helpers/component-events-table.vue'
    import TabPanel from '../components/tab-panel.vue'

    export default {
        components: {
            ComponentPropsTable,
            ComponentEventsTable,
            TabPanel
        },
        data: function(){
            return {
                properties: [
                    { name: 'tabItems', type: 'String', required: 'yes', description: 'Contains tab information. Tab object structure: { value, title }'},
                    { name: 'tabContainerClass', type: 'String', required: 'no', description: 'Sets a class on the tab container to be able to override styling'},
                    { name: 'tabItemClass', type: 'String', required: 'no', description: 'Sets a class on the tab item to be able to override styling'},
                ],
                events: [
                    { name: "tabChanged", args: "tabValue", description: 'Events emitted when new tab is selected. The value of the tab object that is clicked is sent as the event argument'}
                ],
                tabs: [
                    { value: 1, title: "Tab 1" },
                    { value: 2, title: "Tab 2" }
                ],
                defaultTabBarHtml: '<tab-panel :tabItems="tabs" @tabChanged="changeTab"></tab-panel>',
                customTabBarHtml: '<tab-panel :tabItems="tabs" :tabContainerClass="\'my-tab-panel-container\'" :tabItemClass="\'my-tab-item\'" @tabChanged="changeTab"></tab-panel>',
                customCss: '.my-tab-panel-container {\n' +
                            '    text-align: left;\n'+
                            '    padding: 0;\n' +
                            '}\n\n' +
                            '.my-tab-item {\n' +
                            '    padding: 5px;\n' +
                            '    margin:5px;\n' +
                            '    cursor:pointer;\n' +
                            '    font-size: 12px;\n' +
                            '}\n\n' +
                            '.my-tab-item:hover {\n' +
                            '    border-bottom: 2px solid rgb(152, 198, 243, 0.1);\n' +
                            '}\n\n' +
                            '.my-tab-item.active {\n' +
                            '    border-bottom: 2px solid rgb(30, 144, 255);\n' +
                            '    font-weight: bold;\n' +
                            '}'
            }
        }
    }
</script>

<style>
    .my-tab-panel-container {
        text-align: left;
        padding: 0;
    }

    .my-tab-item {
        padding: 5px;
        margin:5px;
        cursor:pointer;
        font-size: 12px;
    }

    .my-tab-item:hover {
        border-bottom: 2px solid rgb(152, 198, 243, 0.1);
    }

    .my-tab-item.active {
        border-bottom: 2px solid rgb(30, 144, 255);
        font-weight: bold;
    }
</style>