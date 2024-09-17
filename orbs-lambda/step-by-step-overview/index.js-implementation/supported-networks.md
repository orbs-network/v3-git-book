# Supported Networks

## EVM

When defining triggers for lambda execution, you must define which blockchain network the lambda executes on. To execute the lambda over multiple networks side by side, define multiple triggers side by side. Upon execution, the trigger event handler will receive an initialized `web3` object that allows to make queries and send transactions on this network.

The following EVM networks are supported:

### **Ethereum mainnet**

Network ID:  `ethereum`\
Explorer: [https://etherscan.io](https://etherscan.io/)

### **Polygon mainnet**

Network ID:  `polygon`\
Explorer: [https://polygonscan.com](https://polygonscan.com/)

### **BNB Chain mainnet (previously Binance Smart Chain)**

Network ID: `bsc`\
Explorer: [https://bscscan.com](https://bscscan.com/)

### **Avalanche mainnet**

Network ID: `avalanche`\
Explorer: [https://snowtrace.io](https://snowtrace.io/)

### **Fantom mainnet**

Network ID: `fantom`\
Explorer: [https://ftmscan.com](https://ftmscan.com/)
