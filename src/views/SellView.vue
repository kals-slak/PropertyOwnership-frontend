<template >
    <div class="form">
        <el-form :model="form" label-width="120px">
            <el-form-item label="Property Detail">
                <el-input v-model="form.details" />
            </el-form-item>
            <el-form-item label="Price">
                <el-input v-model="form.rate" />
            </el-form-item>
            <el-button type="success" @click="sellProperty" >Sell</el-button>
    </el-form>

    </div>
     
</template>

<style>
.form{
   margin: auto;
   /* margin-top: 10%; */

}
.el-input__inner{
    width: 200px !important;
}

</style>

<script setup>
import { ref } from 'vue';
import { ElMessage } from 'element-plus';
import Web3 from 'web3';
// import {hi} from '../views/BuyView.vue';

// console.log(hi);

const form = ref({
  details: '',
  rate:0,
});


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


const successMessage = () => {
  ElMessage({
    message: 'Congrats, Your House is Added.',
    type: 'success',
  })
}
const errorMessage = () => {
  ElMessage.error('Oops, something went wrong');
}

const sellProperty=()=>{
  propertyContract.methods.addProperty(form.value.details,form.value.rate).send({from:client.value,gas:3000000}).then(function(tx){
                console.log(tx);
                successMessage();
            }).catch(function(tx){
                console.log(tx);
                errorMessage();
            })
}


// const sellProperty = () =>{
//     alert(form.value.details+" "+form.value.rate );
// }

</script>