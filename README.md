# zkBitcoin Miner Overview

zkBitcoin Miner forked from IwYeo's SoliditySHA3Miner

Designed for developers and enthusiasts looking to mine zkBitcoin, a minable ERC-918 compatible token on zkSync Era.

## System Requirements and Dependencies

The zkBitcoin Miner is built with the following technologies and libraries:

- **.NET 5.0**: Necessary for running the miner. Download from [Microsoft .NET Download](https://dotnet.microsoft.com/download/dotnet/thank-you/runtime-5.0.5-windows-x64-installer).
- **VC++ 2019**: Required for certain cryptographic functions. Download from [Visual Studio](https://aka.ms/vs/16/release/vc_redist.x64.exe) or [Microsoft Support](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads).
- **nVidia CUDA SDK 10.2** (64-bit): For nVidia GPU support. Ensure your nVidia drivers are version 396 or above. [nVidia Drivers](https://www.nvidia.com/drivers/beta).
- **AMD APP SDK v3.0.130.135** (OpenCL): For AMD GPU support. Download from [Google Drive](https://drive.google.com/file/d/1P5jqRGbWRW1l5vxlm8MqaQRBKpUNUSyf/view?usp=sharing).
- **gcc 4.8.5**: For compiling on Linux-based systems.

## Getting Started with Solo Mining

### Prerequisites

Before starting with zkBitcoin mining, ensure you have the following:

- **.NET Core Runtime**: For Windows, download from [Microsoft .NET Download](https://dotnet.microsoft.com/download/dotnet/thank-you/runtime-5.0.5-windows-x64-installer). 
- **Nvidia or AMD GPU Drivers**: Ensure you have the latest drivers installed that support CUDA or OpenCL, respectively.

For Ubuntu, Go to the [Linux zkBitcoin Miner Github]([https://aka.ms/vs/16/release/vc_redist.x64.exe](https://github.com/ZKBitcoinToken/Linux-CPU-GPU-zkBitcoin-Miner)

### Configuration

1. Open the `_zkBitcoinMiner.conf` file for editing.
2. Update the following configuration parameters as needed:
   - `minerAddress`: Your zkSync Era (Ethereum) address for mining rewards (must include the '0x' prefix).
   - `privateKey`: Your private key associated with the mining zkSync Era (Ethereum) address.
   - `MinZKBTCperMint` and `MaxZKBTCperMint`: Set your desired minimum and maximum zkBitcoin rewards per mint transaction. (Note, if omitted, this will default to `250` and `500` zkBitcoin respectively)
   - `HowManyBlocksAWAYFromAdjustmentToSendMinimumZKBTC`: Adjust this value based on how many blocks away from the adjustment you wish to start sending the minimum zkBitcoin. This can be a value from 0 - 2000 depending on how many other users are submitting. (Note, if omitted, this will default to `200` blocks)
   - `web3api`: Replace with your own web3api if needed; defaults to the provided Alchemy account for testing.

3. Save your changes to `_zkBitcoinMiner.conf`.

### Starting the Miner

To begin mining:
1. Run the `_zkBitcoin Miner Start.bat` file in the miner's directory.
2. Ensure you have a minimal amount of ZK Sync Era Ethereum in your account to start.

## Usage and Options

The miner supports various command-line options for customization, including but not limited to enabling CPU mining, setting GPU intensity, specifying mining pools, and adjusting gas prices for transactions.

```
Usage: _zkBitcoinMiner [OPTIONS]

Options:

-  help                    Display this help text and exit

-  allowCPU                Allow to use CPU, may slow down system (default: false)

-  cpuAffinity             Comma separated list of CPU affinity ID to use (default: all odd number logical processors)

-  allowIntel              Allow to use Intel GPU (OpenCL) (default: false)

-  allowAMD                Allow to use AMD GPU (OpenCL) (default: true)

-  allowCUDA               Allow to use Nvidia GPU (CUDA) (default: true)

-  intelIntensity          GPU (Intel OpenCL) intensity (default: 17, decimals allowed)

-  listAmdDevices          List of all AMD (OpenCL) devices in this system and exit (device ID: GPU name)

-  amdDevice               Comma separated list of AMD (OpenCL) devices to use (default: all devices)

-  amdIntensity            GPU (AMD OpenCL) intensity (default: 24.056, decimals allowed)

-  listCudaDevices         List of all CUDA devices in this system (device ID: GPU name)

-  cudaDevice              Comma separated list of CUDA devices to use (default: all devices)

-  cudaIntensity           GPU (CUDA) intensity (default: auto, decimals allowed)

-  minerJsonAPI            'http://IP:port/' for the miner JSON-API (default: http://127.0.0.1:4078 [0 disabled])

-  minerCcminerAPI         'IP:port' for the ccminer-style API (default: 127.0.0.1:4068 [0 disabled])

-  overrideMaxTarget       (Pool only) Use maximum target and skips query from web3

-  customDifficulty        (Pool only) Set custom difficulity (check with your pool operator)

-  maxScanRetry            Number of retries to scan for new work (default: 3)

-  pauseOnFailedScans      Pauses mining after number of connection fails, including secondary and retries (default: 3)

-  submitStale             Submit stale jobs, may create more rejected shares (default: false)

-  abiFile                 Token abi in a file (default: '0xBTC.abi' in the same folder as this miner)

-  web3api                 User-defined web3 provider URL (default: Infura mainnet provider [dev account, for TESTING PURPOSE only])

-  contract                Token contract address (default: 0xbtc contract address)

-  hashrateUpdateInterval  Interval (miliseconds) for GPU hashrate logs (default: 30000)

-  networkUpdateInterval   Interval (miliseconds) to scan for new work (default: 15000)

-  masterMode              Enable Master mode that virtually acts as a \"pool\" for slave miners connecting to it (default: false [requires admin/sudo mode])

-  masterURL               Master instance IP:port, slave mode if 'masterMode' is false (default: none [if 'masterMode' is true, default: http://{localIP}:4080/])

-  slaveUpdateInterval     (Slave only)Interval (miliseconds) to scan for new work (default: 5000)

-  kingAddress             Add MiningKing address to nonce, only CPU mining supported (default: none)

-  address                 (Pool only) Miner's ethereum address (default: developer's address)

-  privateKey              (Solo only) Miner's private key

-  MinZKBTCperMint         (Solo only) Minimum amount of zkBitcoin to allow the mint to succeed

-  MaxZKBTCperMint         (Solo only) Maxmium amount of zkBitcoin to allow the mint to succeed

-  HowManyBlocksAWAYFromAdjustmentToSendMinimumZKBTC (Solo only) How many blocks way from a readjustment do you want to send MinZKBTCperMint

-  NFTApiURL               (Solo only) URL to the API for NFT minting
  
-  NFTApiPath              (Solo only) Path variable for API to get the NFT contract address or Just the contract address of NFT you want to mint
 
-  NFTApiPathID            (Solo only) Path variable for API to get the NFT ID or Just the NFTs ID you want to mint
  
-  ERC20Addresses          (Solo only) Sepcifies the ERC20 tokens to mint.  Must be in an array with quotes around the contract address
  
-  ETHwithMints            (Solo only) Sepcifies wether to call a cheaper function that doesn't transfer ETH to you from the contract (in case its dust).  Either false or true

-  gasToMine               (Solo only) Gas price to mine in GWei (default: 3, decimals allowed; note: will override lower dynamic gas price)

-  gasLimit                (Solo only) Gas limit to submit proof of work (default: 1704624)

-  gasApiURL               (Solo only) Get dynamic gas price to mine from this JSON API URL (note: leave empty to disable)

-  gasApiPath              (Solo only) JSON path expression to retrieve dynamic gas price value from 'gasApiURL'

-  gasApiMultiplier        (Solo only) Multiplier to dynamic gas price value from 'gasApiURL' => 'gasApiPath' (note: use 0.1 for EthGasStation API)

-  gasApiOffset            (Solo only) Offset to dynamic gas price value from 'gasApiURL' => 'gasApiPath' (after 'gasApiMultiplier', decimals allowed)

-  gasApiMax               (Solo only) Maximum gas price to mine in GWei from API (default: 5, decimals allowed)

-  pool                    (Pool only) URL of pool mining server (default: http://bnbtcpool.crnx.org:80)

-  secondaryPool           (Optional) URL of failover pool mining server

-  logFile                 Enables logging of console output to '{appPath}\\Log\\{yyyy-MM-dd}.log' (default: false)

-  devFee                  Set developer fee in percentage (default: 2.0%, minimum: 2.0%)
```

## License

zkBitcoin Miner is released under the Apache License, Version 2.0. It includes several third-party libraries under their respective licenses:

- **libkeccak-tiny**: [GitHub Repository](https://github.com/coruus/keccak-tiny/)
- **Nethereum**: [License Details](https://github.com/Nethereum/Nethereum/blob/master/LICENSE.md)
- **Json.NET**: [License Details](https://github.com/JamesNK/Newtonsoft.Json/blob/master/LICENSE.md)
- **Common Infrastructure Libraries for .NET**: [License Details](http://netcommon.sourceforge.net/license.html)
- **Bouncy Castle**: [License Details](https://www.bouncycastle.org/licence.html)

## Notes

- Refer to 'GuideForSoloMining.txt' on how to get started.
- Configuration is based on CLI (similar to ccminer), except ".abi" files are required for new tokens (You can manually create one and copy from etherscan.com -> Contract -> Code -> Contract ABI).
- Sample CLI launch parameter can be found in the ".bat" file found together with this miner, please refer to it if you need help.
- Ensure you are mining to the correct address/account. This is YOUR RESPONSIBILITY.
- It is recommended to use your own web3api (e.g. Infura / Geth / Parity) if you solo mine, default value is for TESTING PURPOSES ONLY.
- A default developer fee of 2.0% is applied.
- In the case if the compute load for your GPU is not >= 99%, you can adjust the intensity via (amdIntensity/cudaIntensity/intelIntensity).

Thank you for trying out the zkBitcoin Miner!

## Feedback and Support

We welcome your feedback and suggestions to improve the zkBitcoin Miner. Please submit issues to the GitHub repository or reach out via the zkBitcoin Discord to `Untouchable_Fge#6920`, or find out more on the [zkBitcoin website](https://testnet.zkbitcoin.org/index/).
