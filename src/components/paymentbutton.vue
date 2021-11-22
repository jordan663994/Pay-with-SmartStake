<template>
  <div>
    <md-button
      class="md-raised md-primary"
      v-on:click="
        pay(
          '0x0000000000000000000000000000000000000000',
          '5' + '000000000000000000'
        )
      "
    >
      <strong>pay with sst</strong>
    </md-button>
  </div>
</template>

<script>
import "vue-material";
import { abi, address, address2 } from "./contract.js";
import Contract from "web3-eth-contract";
import utils from "web3-utils";
export default {
  methods: {
    pay: async function (input1, input2) {
      if (
        async () => {
          if (window.ethereum) {
            await window.ethereum.send("eth_requestAccounts");
            Contract.setProvider(window.ethereum);
            try {
              // Request account access if needed
              await window.ethereum.enable();
              // Acccounts now exposed
            } catch (error) {
              console.error(error);
            }
            const contract = new Contract(abi, address);
            const _data = contract.methods
              .transferFrom(window.ethereum.selectedAddress, input1, input2)
              .encodeABI();
            var transactionParameters = {
              nonce: "0x00",
              gasPrice: "0xffff",
              gas: "0xfffff",
              to: address,
              from: window.ethereum.selectedAddress,
              value: "0x00",
              data: _data,
              chainId: "0x1",
            };

            var txHash = await window.ethereum
              .request({
                method: "eth_sendTransaction",
                params: [transactionParameters],
              })
              .then(console.log());
            console.log(txHash);
          } else {
            console.log("404: metamask not found");
          }
          return true;
        }
      ) {
        console.log("payment successful, enter your code below");
      }
    },
  },
  name: "trade",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
a {
  padding: 20px;
  text-decoration: none;
  color: whitesmoke;
  background-color: rgb(0, 26, 255);
}
button {
  background-color: rgb(0, 26, 255);
  color: whitesmoke;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
</style>
