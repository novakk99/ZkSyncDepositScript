# ZkSync Deposi tScript
This script demonstrates how to deposit funds from Ethereum to ZkSync using the ZkSync JavaScript library
const { ethers } = require("ethers");
const { Wallet, getDefaultProvider } = require("zksync");

// Set up your ZkSync provider and wallet
const zkSyncProvider = getDefaultProvider("mainnet");
const privateKey = "your-private-key";
const zkSyncWallet = Wallet.fromEthSigner(new ethers.Wallet(privateKey), zkSyncProvider);

// Specify the token and amount to deposit
const token = "ETH";
const amount = ethers.utils.parseEther("0.5");

// Deposit funds from Ethereum to ZkSync
const deposit = zkSyncWallet.depositToSyncFromEthereum({
  depositTo: zkSyncWallet.address(),
  token,
  amount,
});

// Wait for the deposit to be confirmed
const receipt = await deposit.awaitReceipt();

console.log("Transaction hash:", receipt.transactionHash);
console.log("Deposit complete!");
