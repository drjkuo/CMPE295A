Build process

1. Set up and run a test server
npm install ethereumjs-testrpc web3 and run ./testrpc

2. Upload a compiled contract to the test server
Web3 = require('web3');
web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
code = fs.readFileSync('Solar.sol').toString();
solc = require('solc');
compiledCode = solc.compile(code);
abiDefinition = JSON.parse(compiledCode.contracts[':Solar'].interface);
SolarContract = web3.eth.contract(abiDefinition);
byteCode = compiledCode.contracts[':Solar'].bytecode;
deployedContract = SolarContract.new({data: byteCode, from: web3.eth.accounts[0], gas: 4700000});
contractInstance = SolarContract.at(deployedContract.address);

3. Visit index.html
Because we need a npm file (web3/lib/solidity/coder.js), we run browserify to add the npm file to our client-side js file.
Remberber to change the contract address in index.js before running browserify.
