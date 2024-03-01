## 1/7

Deployment info 

yarn deploy
Compiling 24 Solidity files
Generating typings for: 24 artifacts in dir: typechain-types for target: ethers-v5
Successfully generated 74 typings!
Successfully compiled 24 Solidity files
deploying "MockERC20" (tx: 0x440f516a297828d943c4081a84df545e37f2e6f759fb6ee84a8f3919f351bc49)...: deployed at 0x5FbDB2315678afecb367f032d93F642f64180aa3 with 622433 gas
MockERC20 deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3
deploying "MockERC721" (tx: 0x8136ed0865e1295dbf1eb665392304f443df9799af8cbe28cb372eafb542369f)...: deployed at 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512 with 1215745 gas
MockERC721 deployed to: 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512
deploying "MockERC1155" (tx: 0xfa358c8ae638c25604d673daaba65d8de505b94d2abaed27aa7cccc7739bdd63)...: deployed at 0x9fE46736679d2D9a65F0992F2272dE9f3c7fa6e0 with 1280805 gas
MockERC1155 deployed to: 0x9fE46736679d2D9a65F0992F2272dE9f3c7fa6e0
deploying "CoqInuRugCleaner" (tx: 0x5dfdc051c17602bc0e789e48fabca91981c2dce4f251837509afddd389334c67)...: deployed at 0xCf7Ed3AccA5a467e9e704C703E8D87F634fB0Fc9 with 2756905 gas
CoqInuRugCleaner deployed to: 0xCf7Ed3AccA5a467e9e704C703E8D87F634fB0Fc9
📝 Updated TypeScript contract definition file on ../nextjs/contracts/deployedContracts.ts

## 1/11
deployed to fuji at 0x4A07d41680A1f43D49695dC14790D120D6b783B5
https://testnet.snowtrace.io/tx/0x85f45ef942f6fec93d8979f92ce4b95ebef8d9b49f66459ea96e6475c52f4969?chainId=43113

## 2/27
harpie intergratin:

```
async function validateAddressWithHarpie(address) {
  const apiKey = 'YOUR_API_KEY'; // Replace with your actual API key
  const response = await fetch("https://api.harpie.io/v2/validateAddress", {
    method: "POST",
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      apiKey: apiKey,
      address: address
    })
  });

  if (!response.ok) {
    throw new Error('Failed to validate address');
  }

  const data = await response.json();

  if (data.isMaliciousAddress) {
    console.warn(data.summary); // Or handle malicious address more strictly
    // Implement your logic here to block the address or alert the user
    return false; // Indicating the address should be blocked
  } else {
    // Address is considered safe
    return true; // Indicating the address is allowed
  }
}
```

## 2/28

wrestled with getiing the api working correctly. 
Set up api endpoint in pages/api/validateAddress  - this is on the server side and is how we actually communicate to the api and make requests.
In compoents/scaffol-eth/rainbowkitconnectwalletbutton I put the logic for validateAddress. Once a user connects a wallet it will send the api request with that wallet and if the wallet is blocked it will redirect the user to the pages/blockedPage.

ToDo: API calls 4 times - see if there is a way to get it to 1. Then if a wallet is blocked you should black list it? Or log it out. Or never allow the user to visit a page where they could interact with the contract.

Made the worthless home page, removed some fluff from header/footers, created harvesterc20 & 1155 comoents and put them plus harvest 721 into one page