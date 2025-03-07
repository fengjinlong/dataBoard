<script setup lang="ts">
import { onMounted, reactive, ref } from "vue";
import { Button } from "@/components/ui/button";
const fareNum: {
  value: number;
  value_classification: string;
} = reactive({
  value: 0,
  value_classification: "",
});
const cnn = reactive({ rating: "", value_classification: "", score: 0 });
onMounted(() => {
  fetch("https://api.alternative.me/fng/")
    .then((res) => res.json())
    .then((res) => {
      console.log(res);
      fareNum.value = res.data[0].value;
      fareNum.value_classification = res.data[0].value_classification;
    });

  fetch("https://production.dataviz.cnn.io/index/fearandgreed/graphdata")
    .then((res) => res.json())
    .then((res) => {
      console.log(res);
      cnn.rating = res.fear_and_greed.rating;
      cnn.score = Math.round(res.fear_and_greed.score);
    });

  // fetch("https://pro-api.coinmarketcap.com/v3/fear-and-greed/historical", {
  //   headers: {
  //     "X-CMC_PRO_API_KEY": "2adaa0fe-8df6-4d3b-aca7-06ff0f906c8d",
  //   },
  // })
  //   .then((res) => res.json())
  //   .then((res) => {
  //     console.log(res);
  //   });

  // 2adaa0fe-8df6-4d3b-aca7-06ff0f906c8d
  // X-CMC_PRO_API_KEY
});
const urlArr = ref([
  {
    name: "交易所充值地址",
    url: "https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-depositing-addresses?exchange=binance&window=DAY&priceScale=linear&metricScale=linear&chartStyle=column&sma=0&ema=0",
  },
  {
    name: "交易所提现地址",
    url: "https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-withdrawing-addresses?exchange=binance&window=DAY&priceScale=log&metricScale=linear&chartStyle=line&sma=0&ema=0",
  },
  {
    name: "旷工MPI指数变化",
    url: "https://cryptoquant.com/asset/btc/chart/flow-indicator/miners-position-index-mpi?window=DAY&sma=0&ema=0&priceScale=log&metricScale=linear&chartStyle=column",
  },
  {
    name: "交易所净流量（总）对于现货交易，高值表示抛售压力增加",
    url: "https://cryptoquant.com/asset/btc/chart/exchange-flows/exchange-netflow-total?exchange=binance&window=DAY&sma=0_7&priceScale=log&metricScale=linear&chartStyle=column&ema=0",
  },
  // {
  //   name: "交易所btc转出地址变化",
  //   url: "https://cryptoquant.com/asset/btc/chart/addresses/active-sending-addresses?window=DAY&priceScale=log&metricScale=linear&chartStyle=line&sma=0&ema=0",
  // },
  // {
  //   name: "交易所btc转入地址变化",
  //   url: "https://cryptoquant.com/asset/btc/chart/addresses/active-receiving-addresses?window=DAY&priceScale=log&metricScale=linear&chartStyle=line&sma=0&ema=0",
  // },
]);
// import { ref } from "vue";
</script>

<template>
  <div class="ma">
    <h3>
      <span>alternative: </span>
      <span>{{ fareNum.value_classification }}:{{ fareNum.value }}</span>
    </h3>
    <h3>
      <span>CNN: </span>
      <span>{{ cnn.rating }}: {{ cnn.score }}</span>
    </h3>
    <div class="btns pb-10">
      <Button variant="default" v-for="ele in urlArr" class="mx-4">
        <a :href="ele.url" target="_blank" rel="noopener noreferrer">{{
          ele.name
        }}</a>
      </Button>
    </div>
    <div class="con">
      <div class="item">
        <h4>7天活动地址均值</h4>
        <iframe
          width="100%"
          height="420"
          frameborder="0"
          src="https://www.theblock.co/data/on-chain-metrics/comparison-bitcoin-ethereum-solana/number-of-active-addresses-7dma/embed"
        ></iframe>
      </div>
      <div class="item">
        <h4>加密货币总市值</h4>
        <iframe
          width="100%"
          height="420"
          frameborder="0"
          src="https://www.theblock.co/data/crypto-markets/prices/crypto-total-marketcap/embed"
        ></iframe>
      </div>
    </div>
    <h1>BTC</h1>
    <div class="con">
      <div class="item">
        <h4>BTC 活跃地址（7DMA）</h4>
        <iframe
          width="100%"
          height="420"
          frameborder="0"
          src="https://www.theblock.co/data/on-chain-metrics/bitcoin/number-of-active-addresses-on-the-bitcoin-network-7dma/embed"
          title="Number of Active Addresses on the Bitcoin Network (7DMA)"
        ></iframe>
      </div>
      <div class="item">
        <h4>BTC 链上交易量（7DMA）</h4>
        <iframe
          width="100%"
          height="420"
          frameborder="0"
          src="https://www.theblock.co/data/on-chain-metrics/bitcoin/bitcoins-adjusten-on-chain-volume-daily/embed"
          title="Bitcoin's On-Chain Volume (Daily, 7DMA)"
        ></iframe>
      </div>
    </div>
    <h1>链上数据比较</h1>

    <div class="con">
      <div class="item">
        <h4>BTC ETH 链上交易量（7DMA）</h4>
        <iframe
          width="100%"
          height="420"
          frameborder="0"
          src="https://www.theblock.co/data/on-chain-metrics/comparison-bitcoin-ethereum-solana/adjusted-on-chain-volume-daily/embed"
        ></iframe>
      </div>
      <div class="item">
        <h4>以太坊与Solana TVL 对比</h4>
        <iframe
          width="100%"
          height="420"
          frameborder="0"
          src="https://www.theblock.co/data/on-chain-metrics/comparison-bitcoin-ethereum-solana/adjusted-on-chain-volume-daily/embed"
        ></iframe>
      </div>
    </div>
    <h1>Solana 数据</h1>
    <div class="con">
      <div class="item">
        <h4>Solana 链上活跃地址（7DMA）</h4>
        <iframe
          width="100%"
          height="420"
          frameborder="0"
          src="https://www.theblock.co/data/on-chain-metrics/solana/number-of-active-addresses-on-the-solana-network-daily-7dma/embed"
          title="Number of Active Addresses on the Solana Network (Daily, 7DMA)"
        ></iframe>
      </div>
      <div class="item">
        <h4>Solana 每周交易费用</h4>
        <iframe
          width="100%"
          height="420"
          frameborder="0"
          src="https://www.theblock.co/data/on-chain-metrics/solana/solana-transaction-fee-breakdown/embed"
          title="Weekly Solana Transaction Fee Breakdown"
        ></iframe>
      </div>
    </div>
  </div>
</template>

<style scoped>
.ma {
  width: 100%;
}
.con {
  width: 100%;
  display: flex;
}
.item {
  width: 50%;
  text-align: center;
}
</style>
