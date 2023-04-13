<template>
  <!-- <div v-for="t in testing" :key="t[0]"> -->
   
          <!-- <h4>Owner: {{t[1]}}</h4>
          <p><strong>About:</strong>{{ t[2]}}</p>
          <h4>Price: {{t[3]}} Wei</h4> -->
  <!-- </div> -->
  <el-row :gutter="6">
    <el-col
      v-for="t in testing"
      :key="t[0]"
      :span="6"
      
    >
      <el-card :body-style="{ padding: '10px' }">
        <img
          src="https://i.pinimg.com/564x/09/c2/a8/09c2a8970c791f8238877756434447ff.jpg"
          class="image"
        />
        <div >
              <div style="display:flex ; align-items: baseline;margin: 0;padding: 0;">
                <h4>Owner:</h4>
                <p style="font-size: small;">{{t[1]}}</p>
              </div> 
              <div style="display:flex ; align-items: baseline;">
                <h4>Price:</h4>
                <p >{{t[3]}}</p>
              </div>  
			  <el-button @click="buyProperty(t[0])" type="success">Buy Now</el-button> 
        </div>
        
      </el-card>
    </el-col>
  </el-row>
</template>


<style>
.time {
  font-size: 12px;
  color: #999;
}

.bottom {
  margin-top: 13px;
  line-height: 12px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.button {
  padding: 0;
  min-height: auto;
}

.image {
  width: 100%;
  display: block;
}
</style>


<script setup>

import { ref } from 'vue';
import Web3 from 'web3';

const testing= ref([]);
const web3 = new Web3(Web3.givenProvider);
const client= ref("");
web3.eth.getAccounts().then(function(acc){ client.value= acc[0];});


// const address= "0xb7E5Eec364B3cb9D7512460d2E036a283BD09115";
const address= "0x0067bF2CDB37b1f0690170C39fF0c0c5CaA06127";
// const propertyContract= new web3.eth.Contract([
// 	{
// 		"inputs": [],
// 		"stateMutability": "nonpayable",
// 		"type": "constructor"
// 	},
// 	{
// 		"inputs": [],
// 		"name": "addId",
// 		"outputs": [],
// 		"stateMutability": "nonpayable",
// 		"type": "function"
// 	},
// 	{
// 		"inputs": [
// 			{
// 				"internalType": "string",
// 				"name": "_details",
// 				"type": "string"
// 			},
// 			{
// 				"internalType": "uint256",
// 				"name": "_rate",
// 				"type": "uint256"
// 			}
// 		],
// 		"name": "addProperty",
// 		"outputs": [],
// 		"stateMutability": "nonpayable",
// 		"type": "function"
// 	},
// 	{
// 		"inputs": [
// 			{
// 				"internalType": "uint256",
// 				"name": "",
// 				"type": "uint256"
// 			}
// 		],
// 		"name": "assets",
// 		"outputs": [
// 			{
// 				"internalType": "uint256",
// 				"name": "propertyID",
// 				"type": "uint256"
// 			},
// 			{
// 				"internalType": "address payable",
// 				"name": "owner",
// 				"type": "address"
// 			},
// 			{
// 				"internalType": "string",
// 				"name": "details",
// 				"type": "string"
// 			},
// 			{
// 				"internalType": "uint256",
// 				"name": "rate",
// 				"type": "uint256"
// 			}
// 		],
// 		"stateMutability": "view",
// 		"type": "function"
// 	},
// 	{
// 		"inputs": [
// 			{
// 				"internalType": "uint256",
// 				"name": "_propertyID",
// 				"type": "uint256"
// 			}
// 		],
// 		"name": "buyProperty",
// 		"outputs": [],
// 		"stateMutability": "payable",
// 		"type": "function"
// 	},
// 	{
// 		"inputs": [],
// 		"name": "id",
// 		"outputs": [
// 			{
// 				"internalType": "uint256",
// 				"name": "",
// 				"type": "uint256"
// 			}
// 		],
// 		"stateMutability": "view",
// 		"type": "function"
// 	},
// 	{
// 		"inputs": [
// 			{
// 				"internalType": "uint256",
// 				"name": "amount",
// 				"type": "uint256"
// 			}
// 		],
// 		"name": "refundPayment",
// 		"outputs": [],
// 		"stateMutability": "nonpayable",
// 		"type": "function"
// 	},
// 	{
// 		"inputs": [
// 			{
// 				"internalType": "uint256",
// 				"name": "_propertyID",
// 				"type": "uint256"
// 			}
// 		],
// 		"name": "removeProperty",
// 		"outputs": [],
// 		"stateMutability": "nonpayable",
// 		"type": "function"
// 	},
// 	{
// 		"inputs": [],
// 		"name": "sc_owner",
// 		"outputs": [
// 			{
// 				"internalType": "address payable",
// 				"name": "",
// 				"type": "address"
// 			}
// 		],
// 		"stateMutability": "view",
// 		"type": "function"
// 	},
// 	{
// 		"inputs": [
// 			{
// 				"internalType": "uint256",
// 				"name": "_propertyID",
// 				"type": "uint256"
// 			},
// 			{
// 				"internalType": "string",
// 				"name": "_details",
// 				"type": "string"
// 			},
// 			{
// 				"internalType": "uint256",
// 				"name": "_rate",
// 				"type": "uint256"
// 			}
// 		],
// 		"name": "updateProperty",
// 		"outputs": [],
// 		"stateMutability": "nonpayable",
// 		"type": "function"
// 	},
// 	{
// 		"inputs": [],
// 		"name": "viewAllProperties",
// 		"outputs": [
// 			{
// 				"components": [
// 					{
// 						"internalType": "uint256",
// 						"name": "propertyID",
// 						"type": "uint256"
// 					},
// 					{
// 						"internalType": "address payable",
// 						"name": "owner",
// 						"type": "address"
// 					},
// 					{
// 						"internalType": "string",
// 						"name": "details",
// 						"type": "string"
// 					},
// 					{
// 						"internalType": "uint256",
// 						"name": "rate",
// 						"type": "uint256"
// 					}
// 				],
// 				"internalType": "struct PropertyOwnerShip.Property[]",
// 				"name": "",
// 				"type": "tuple[]"
// 			}
// 		],
// 		"stateMutability": "view",
// 		"type": "function"
// 	}
// ],address);

const propertyContract= new web3.eth.Contract([
	{
		"inputs": [],
		"name": "addId",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "string",
				"name": "_details",
				"type": "string"
			},
			{
				"internalType": "uint256",
				"name": "_rate",
				"type": "uint256"
			}
		],
		"name": "addProperty",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "_propertyID",
				"type": "uint256"
			}
		],
		"name": "buyProperty",
		"outputs": [],
		"stateMutability": "payable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "amount",
				"type": "uint256"
			}
		],
		"name": "refundPayment",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "_propertyID",
				"type": "uint256"
			}
		],
		"name": "removeProperty",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [],
		"stateMutability": "nonpayable",
		"type": "constructor"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "_propertyID",
				"type": "uint256"
			},
			{
				"internalType": "string",
				"name": "_details",
				"type": "string"
			},
			{
				"internalType": "uint256",
				"name": "_rate",
				"type": "uint256"
			}
		],
		"name": "updateProperty",
		"outputs": [],
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"name": "assets",
		"outputs": [
			{
				"internalType": "uint256",
				"name": "propertyID",
				"type": "uint256"
			},
			{
				"internalType": "address payable",
				"name": "owner",
				"type": "address"
			},
			{
				"internalType": "string",
				"name": "details",
				"type": "string"
			},
			{
				"internalType": "uint256",
				"name": "rate",
				"type": "uint256"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "id",
		"outputs": [
			{
				"internalType": "uint256",
				"name": "",
				"type": "uint256"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "sc_owner",
		"outputs": [
			{
				"internalType": "address payable",
				"name": "",
				"type": "address"
			}
		],
		"stateMutability": "view",
		"type": "function"
	},
	{
		"inputs": [],
		"name": "viewAllProperties",
		"outputs": [
			{
				"components": [
					{
						"internalType": "uint256",
						"name": "propertyID",
						"type": "uint256"
					},
					{
						"internalType": "address payable",
						"name": "owner",
						"type": "address"
					},
					{
						"internalType": "string",
						"name": "details",
						"type": "string"
					},
					{
						"internalType": "uint256",
						"name": "rate",
						"type": "uint256"
					}
				],
				"internalType": "struct PropertyOwnerShip.Property[]",
				"name": "",
				"type": "tuple[]"
			}
		],
		"stateMutability": "view",
		"type": "function"
	}
],address);
propertyContract.methods.viewAllProperties().call().then(function(data){
    testing.value= data;
});


const buyProperty=(id)=>{
	console.log(testing.value);
  propertyContract.methods.buyProperty(id).send({from:client.value,gas:3000000,value:testing.value[id][3]}).then(function(tx){
                console.log(tx);
            }).catch(function(tx){
                console.log(tx);
            })
}

// trans owernship
// const buyProperty=()=>{
//   propertyContract.methods.addProperty("testingg",10).send({from:client.value}).then(function(tx){
//                 console.log(tx);
//             }).catch(function(tx){
//                 console.log(tx);
//             })
// }
console.log("buy rendered");
</script>