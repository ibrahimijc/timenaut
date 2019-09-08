<template>
    <div id="app" class="content">
        <navigation id="navigation" :items=navigationItems :switchPage="switchPage"/>
        <app-content id="content" :page="page"/>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import AppContent from './components/content.vue';
    import Navigation from './components/navigation.vue';
    import Dashboard from "@/components/dashboard.vue";
    import Processes from "@/components/processes.vue";
    import Settings from "@/components/settings.vue";
    import {Updateable} from "@/components/Updateable";

    interface PageComponent {
        new (): Updateable;
    }

    type NavigationItem = {
        icon: string,
        iconAlt: string,
        page: PageComponent
    }

    @Component({
        components: {
            Navigation,
            AppContent,
        },
    })
    export default class App extends Vue {
        page: PageComponent = Dashboard;

        navigationItems: NavigationItem[] = [
            {icon: 'dashboard', iconAlt: 'dashboard', page: Dashboard},
            {icon: 'query_builder', iconAlt: 'processes', page: Processes},
            {icon: 'settings', iconAlt: 'settings', page: Settings}
        ];

        switchPage(newPage: PageComponent) {
            this.page = newPage;
        }
    }
</script>

<style>
    @font-face {
        font-family: "Montserrat";
        src: url("assets/fonts/Montserrat-Regular.ttf") format("truetype");
    }

    html {
        height: 100%;
        overflow-x: hidden !important;
        overflow-y: hidden !important;
    }

    body {
        margin: 0;
        background-color: #D9D9D9;
        min-height: 100%;
        max-height: 100%;
    }

    #app {
        font-family: Montserrat, 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-bottom: 0;
        height: 100%;
    }

    #app {
        display: grid;
        grid-template-columns: 60px auto;
        grid-template-rows: 100%;
        height: 100vh;
    }

    #navigation {
        position: fixed;
        width: 60px;
        height: 100%;
    }

    #content {
        grid-column: 2 / 3;
    }
</style>