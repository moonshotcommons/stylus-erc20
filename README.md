# 使用 Stylus 发布 ERC20 合约

## 设置开发环境变量
```bash
export ARB_DEMO=your_address # 您的测试网账户地址
export PRIVATE_KEY=your_private_key # 您的账户私钥
export ARB_RPC=https://sepolia-rollup.arbitrum.io/rpc # Arbitrum Sepolia RPC
```

### 1. 获取代码
```bash
git clone git@github.com:moonshotcommons/stylus-erc20.git
```

### 2. 编译（无需 Docker 环境）
```bash
cargo stylus check -e https://sepolia-rollup.arbitrum.io/rpc
```

### 3. 部署（需要启动 Docker）
```bash
cargo stylus deploy --endpoint=$ARB_RPC --private-key=$PRIVATE_KEY --estimate-gas
```

### 4. 验证合约 
```bash
cargo stylus verify --deployment-tx=0xba2baaafbe2746816a4fbb052e7cdbf7bfafa31693b78cae5734a831d58f2c33 --endpoint=$ARB_RPC
```

### 5. 导出 ABI
```bash
cargo stylus export-abi
```

### 6. 合约交互
#### 使用以下命令铸造代币：
```bash
cast send --rpc-url $ARB_RPC --private-key $PRIVATE_KEY 0xcd7b9304c6ce5531d92b3ea481f62851c533825d "mint(uint256)" 6000000000000000000
```

#### 查询指定地址的代币余额：
```bash
cast call --rpc-url $ARB_RPC 0xcd7b9304c6ce5531d92b3ea481f62851c533825d "balanceOf(address)" $ARB_DEMO
```

#### 将余额转换为十进制格式：
```bash
cast to-dec $(cast call --rpc-url $ARB_RPC 0xcd7b9304c6ce5531d92b3ea481f62851c533825d "balanceOf(address)" $ARB_DEMO)
```