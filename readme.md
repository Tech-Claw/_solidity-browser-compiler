This is example how to use: 


```javascript
import React from 'react'
import { solidityCompiler } from 'solidity-browser-compiler';

const Homepage = () => {
  const compile = async () => {
    const version = 'soljson-v0.8.8+commit.dddeac2f.js';
    const useOptimization = true;
    const runs = 200;
    const contract = `
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.8;
    
    contract Counter {
        uint public count;
        
        // Function to get the current count
        function get() public view returns (uint) {
            return count;
        }
        
        // Function to increment count by 1
        function inc() public {
            count += 1;
        }
        
        // Function to decrement count by 1
        function dec() public {
            // This function will fail if count = 0
            count -= 1;
        }
    }`
    const result = await solidityCompiler({
      version: `https://binaries.soliditylang.org/bin/${version}`,
      contractBody: contract,
      options: { optimizer: { enabled: useOptimization, runs: runs } }
    });
    console.info(result);
  }
  return (
    <div>
      <button onClick={compile}>Compile</button>
    </div>
  )
}

export default Homepage
```

abi, evm, metadata, storage layout is found in: 
`result.contracts.Compiled_Contracts.<YOUR_CONTRACT_NAME>.The thing you need`   
incase there is an error, result will contain two entries: `result.errors` and `result.sources`