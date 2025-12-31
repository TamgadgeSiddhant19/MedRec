# MedRec — Medical Data Access Control (Blockchain + IPFS)

MedRec is a proof-of-concept platform that demonstrates privacy-preserving medical data storage and access control using blockchain smart contracts and IPFS instead of a traditional centralized database. The project uses Ethereum (Truffle) for smart contracts, IPFS for off-chain file storage, and a React frontend to interact with the contracts.

Key ideas

- Patient medical records (or encrypted pointers to them) are stored on IPFS.
- Access control (who can read which record) is managed on-chain using Ethereum smart contracts.
- The Ethereum blockchain stores metadata and access grants; the heavy data lives in IPFS to keep on-chain costs low.
- The frontend interacts with the smart contract (via web3) and with the IPFS node or gateway to upload/retrieve files.

Features

- Register patients and providers
- Patients grant and revoke access to their records
- Records are stored on IPFS; only the IPFS CID and metadata are stored on-chain
- Example React-based UI for uploading files, requesting access, and viewing shared records

Repository structure (typical)

- contracts/        — Solidity contracts (Truffle)
- migrations/       — Truffle migration scripts
- test/             — Contract tests (Mocha/Chai)
- client/           — React frontend
- scripts/          — Utility scripts (IPFS helpers, deployment helpers)
- README.md         — This file

Prerequisites

- Node.js >= 14
- npm or yarn
- Truffle (globally recommended) or use npx
- Ganache (local blockchain) or an Ethereum testnet (e.g., Goerli) and an RPC provider
- IPFS: local daemon (go-ipfs) or a remote gateway / provider (Infura, Pinata)

Getting started — local development (recommended)

1. Clone the repo

   git clone https://github.com/TamgadgeSiddhant19/MedRec.git
   cd MedRec

2. Install dependencies

   # root (if any)
   npm install

   # client
   cd client
   npm install
   cd ..

3. Start a local blockchain

   - Install Ganache GUI or use Ganache CLI
   - Start Ganache and note the RPC URL (usually http://127.0.0.1:7545)

4. Start or configure IPFS

   Option A — Local IPFS
   - Install go-ipfs and run `ipfs init` then `ipfs daemon`

   Option B — Infura / Pinata
   - Create an account and get your project credentials

5. Configure environment variables

   Create a `.env` file in the project root or in `client/` with values similar to:

   REACT_APP_WEB3_PROVIDER=http://127.0.0.1:7545
   REACT_APP_IPFS_API=http://127.0.0.1:5001
   REACT_APP_CONTRACT_ADDRESS=            # (filled after migration)

   If using Infura/Pinata, set the IPFS API URL and credentials as required by your client code.

6. Compile and migrate smart contracts

   # compile
   truffle compile

   # migrate to local network (make sure Truffle config points to Ganache)
   truffle migrate --network development

   After migration, copy the deployed contract address into your `.env` or client config.

7. Start the React client

   cd client
   npm start

   The app should open in the browser and connect to your local blockchain and IPFS node based on environment configuration.

Security & privacy notes

- Encrypt sensitive files before uploading to IPFS if they must remain confidential. IPFS content is public by default.
- The smart contract should only store metadata and access control pointers (CIDs), not raw medical data.
- Consider using off-chain encryption keys shared via secure channels or KMS.

Testing

- Run contract tests with Truffle:

  truffle test

- Add Jest/React testing for the frontend in `client/` as needed.

Deployment

- Deploy smart contracts to a testnet/mainnet using Truffle configuration and an RPC provider (e.g., Infura/Alchemy).
- Use a production IPFS pinning provider (Pinata/Infura) to ensure long-term availability of CIDs.

Contributing

Contributions are welcome! Please open issues or PRs. Typical contributions:

- Improve access-control logic in contracts
- Add encryption key management patterns
- Improve the React UI and UX
- Add tests and CI

License

Specify a license for the project (e.g., MIT). Add a LICENSE file if you choose a permissive license.

Contact

For questions, open an issue or contact the repository owner.


---

(README added/updated by GitHub Copilot)
