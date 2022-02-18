<template>
<trading-vue :data="chart"></trading-vue>
</template>
<script>

import { TradingVue, DataCube } from 'trading-vue-js';

var end = Date.now();
var start = end - (24 * 60 * 60 * 1000);
var msg = {
    "jsonrpc": "2.0",
    "method": "public/get_tradingview_chart_data",
    "id": 42,
    "params" : {
        "instrument_name" : "BTC-PERPETUAL",
        "start_timestamp" : start,
        "end_timestamp" : end,
        "resolution" : "30"
    }
};
var ws = new WebSocket('wss://test.deribit.com/ws/api/v2');
ws.onmessage = function (e) {
    // do something with the response...
    const res = JSON.parse(e.data);
    const result = res.result;
    
    var data = [];
    for (var i = 0; i < result.ticks.length; i++) {
        data[i] = [result.ticks[i], result.open[i], result.high[i], result.low[i], result.close[i], result.volume[i]];
    }
   
    dc.set('chart', {
        type: "Candles",
        data: data,
        settings: {}
    });
};
ws.onopen = function () {
    ws.send(JSON.stringify(msg));
};

const dc = new DataCube();

export default {
    components: { TradingVue },
    data() {
        return {
            chart: dc
        }
    }
}
</script>