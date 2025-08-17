## Farm Assuree – Web3 Farmer–Buyer Marketplace

Farm Assure which is a blockchain-powered contract farming marketplace that bridges the gap between farmers and buyers, ensuring secure, transparent, and fair trade, and while also giving farmers peace of mind that their crop will definitely be sold at a fair price without worrying about market uncertainties.


### Features
- Farmer dashboard: create, manage listings, track requests and orders
- Buyer dashboard: browse crops, search/filter, request to buy, confirm delivery
- Optional bidding flow for buyers
- IPFS image uploads via Pinata
- Modern, responsive UI (MUI + framer-motion + theme toggle)

### Tech Stack
- Frontend: React + Vite, MUI, framer-motion, React Router
- Web3: ethers/web3, MetaMask
- IPFS: Pinata
- Contracts: Solidity + Truffle

### Project Structure

FarmAssure/
  contract/              # Truffle project (Solidity contracts, migrations)
  frontend/              # React + Vite web app
  README.md              # This file


### Prerequisites
- Node.js 18+ and npm
- Git
- MetaMask browser extension
- Truffle (globally): npm i -g truffle
- Local blockchain (Ganache) or a testnet (e.g., Sepolia)
- Pinata account (for IPFS images)

### 1) Smart Contracts – Local Setup
1. Start Ganache (HTTP RPC at http://127.0.0.1:7545 or 8545)
2. Compile and migrate with Truffle:
bash
cd contract
truffle compile
truffle migrate --network development

3. Note the deployed contract address from the migration output.
4. Update the frontend to use the deployed address:
   - frontend/src/pages/FarmerDashboard.jsx → CONTRACT_ADDRESS
   - frontend/src/pages/BuyerDashboard.jsx → CONTRACT_ADDRESS

If you deploy to a testnet, configure truffle-config.js with your RPC and key, then run truffle migrate --network <network> and use that address instead.

### 2) Frontend – Development
Install and run the web app with Vite:
bash
cd frontend
npm install
npm run dev

Vite will print a local URL (e.g., http://localhost:5173). Open it in a browser with MetaMask enabled.

### 3) IPFS (Pinata) Configuration
The project currently includes direct Pinata usage in frontend/src/services/pinataService.js.
- For hackathon demos it may work as-is, but you should replace hardcoded keys with environment variables before any public deployment.
- Recommended: create frontend/.env.local and reference variables in code (Vite uses import.meta.env):
bash
# frontend/.env.local
VITE_PINATA_JWT=replace_with_your_jwt

Then, in pinataService.js, read from import.meta.env.VITE_PINATA_JWT (and do not commit secrets).

### 4) Build & Preview
Create an optimized production build and preview it locally:
bash
cd frontend
npm run build
npm run preview


### 5) Common Issues & Fixes
- MetaMask not connecting:
  - Ensure your browser has MetaMask and you’re on the same network as the deployed contract.
- Wrong contract address:
  - If UI loads but actions fail, verify CONTRACT_ADDRESS in both dashboards matches your latest deployment.
- IPFS images not showing:
  - Check Pinata keys/JWT and network connectivity. As a fallback, try alternate gateways.
- CORS or mixed-content issues on testnets:
  - Use HTTPS RPC endpoints and valid gateways.

### Scripts (frontend)
- npm run dev – start Vite dev server
- npm run build – production build
- npm run preview – preview the production build

### Deploying to Testnet (optional)
- Add a network to contract/truffle-config.js (RPC, chainId, accounts)
- truffle migrate --network <name>
- Update CONTRACT_ADDRESS in the frontend

### License
For hackathon/demo usage. Add your preferred license if publishing widely.
