---
{
  "name": "dogeclone-transfer",
  "version": "1.0.0",
  "scripts": {
    "send": "npx hardhat run scripts/send.js --network bsctest"
  },
  "dependencies": {
    "@nomicfoundation/hardhat-toolbox": "^3.0.0",
    "dotenv": "^16.3.1",
    "hardhat": "^2.19.0"
  }
}
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();

module.exports = {
  solidity: "0.8.20",
  networks: {
    bsctest: {
      url: "https://data-seed-prebsc-1-s1.binance.org:8545/",
      accounts: [process.env.PRIVATE_KEY]
    }
  }
};
const tokenAddress = "COLE_AQUI_O_SEU_CONTRATO";
const recipient = "0x84f35bf7f46d289345a60f98b93e22ff0d82ebd3";
const { ethers } = require("hardhat");

async function main() {
  const tokenAddress = "COLE_AQUI_O_SEU_CONTRATO";
  const recipient = "0x84f35bf7f46d289345a60f98b93e22ff0d82ebd3";

  // Quantidade a enviar:
  const amount = ethers.parseUnits("1000000000", 18); // 1 bilhão de DOGECLONE

  // Carrega o contrato
  const token = await ethers.getContractAt("DogeClone", tokenAddress);

  console.log("Enviando tokens...");
  const tx = await token.transfer(recipient, amount);

  console.log("Tx enviada:", tx.hash);
  await tx.wait();

  console.log("Transferência confirmada!");
}

main().catch((error) => {
  console.error(error);
  process.exit(1);
});
PRIVATE_KEY=SUA_CHAVE_PRIVADA_AQUI
npm install
npm run send
npx hardhat run scripts/send.js --network bsctest
