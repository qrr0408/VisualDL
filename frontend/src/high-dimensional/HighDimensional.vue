<template>
    <div class="visual-dl-page-container">
        <div class="visual-dl-page-left">
            <ui-chart
                    :config="config"
                    :displayWordLabel="config.displayWordLabel"
                    :searchText="config.searchText"
                    :embedding_data="embedding_data"
            ></ui-chart>
        </div>
        <div class="visual-dl-page-right">
            <div class="visual-dl-page-config-container">
                <ui-config
                    :config="config"
                ></ui-config>
            </div>
        </div>
    </div>
</template>

<script>
import {getHighDimensionalDatasets} from '../service';
import autoAdjustHeight from '../common/util/autoAdjustHeight';
import Config from './ui/Config'
import Chart from './ui/Chart';

export default {
    components: {
        'ui-config': Config,
        'ui-chart': Chart,
    },
    name: 'HighDimensional',
    data () {
        return {
            config: {
                searchText: '',
                displayWordLabel: true,
                running: true
            },
            embedding_data: []
        }
    },
    created() {
    	    getHighDimensionalDatasets().then(({errno, data}) => {
            this.embedding_data = data.embedding;
        });
    },
    mounted() {
        autoAdjustHeight();
    },
    methods: {
    }
};

</script>

<style lang="stylus">

</style>
