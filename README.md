# Drosera-Network Installing only free VPS (github space , replit , google clone , etc)
If you want install on VPS use tutorial from [0xmoei](https://github.com/0xmoei/Drosera-Network)
In this Guide, we contribute to Drosera testnet by:
1. Installing the CLI
2. Setting up a vulnerable contract
3. Deploying a Trap on testnet
4. Connecting an operator to the Trap

# Recommended System Requirements
* 2 CPU Cores
* 4 GB RAM
* 20 GB Disk Space

Official [Discord](https://discord.gg/UXAdpTYjgr)

### Install Dependecies

## Trap Setup

## 1. Configure Enviorments
**Drosera CLI**:
```bash
curl -L https://app.drosera.io/install | bash
```
```
source /home/<username>/.bashrc
```
Change your <username>
OR you can see this command from detected after installing
![image](https://github.com/user-attachments/assets/6910ffe7-5d45-4a64-8cf9-4b84e370c9f8)
```
droseraup
```

**Foundry CLI**:
```
curl -L https://foundry.paradigm.xyz | bash
```
```
source /home/<username>/.bashrc
```
Change your <username>
OR you can see this command from detected after installing
![image](https://github.com/user-attachments/assets/6910ffe7-5d45-4a64-8cf9-4b84e370c9f8)
```
foundryup
```

**Bun:**
```
curl -fsSL https://bun.sh/install | bash
```

---

## 2. Deploy Contract & Trap
```bash
mkdir my-drosera-trap
```
```bash
cd my-drosera-trap
```
**Replace `Github_Email` & `Github_Username`:**
```bash
git config --global user.email "Github_Email"
git config --global user.name "Github_Username"
```
**Initialize Trap**:
```
forge init -t drosera-network/trap-foundry-template
```
**Compile Trap**:
```bash
curl -fsSL https://bun.sh/install | bash
bun install
```
```bash
forge build
```
> skip warnings!

**Deploy Trap**:
```bash
DROSERA_PRIVATE_KEY=xxx drosera apply
```
* Replace `xxx` with your EVM wallet `privatekey` (Ensure it's funded with `Holesky ETH`)
* Enter the commamd, when prompted, write `ofc` and press Enter.

![image](https://github.com/user-attachments/assets/6d1161f1-4423-4ce6-a1a2-77ce567186dc)

---

## 3. Check Trap in Dashboard
1- Connect your Drosera EVM wallet: https://app.drosera.io/

2- Click on `Traps Owned` to see  your deployed Traps OR search your Trap address.

![image](https://github.com/user-attachments/assets/9c39eea0-0aaf-417d-8552-765ff33f8a5e)

---

## 4. Bloom Boost Trap
Open your Trap on Dashboard and Click on `Send Bloom Boost` and deposit some `Holesky ETH` on it.

![image](https://github.com/user-attachments/assets/2f5216fd-fdf9-4732-96d0-959b3fbce479)

## 5. Fetch Blocks
```bash
drosera dryrun
```

---

<h1 align="center">Operator Setup</h1>

## 1. Whitelist Your Operator
**1- Edit Trap configuration:**
```bash
cd ~
```
```bash
cd my-drosera-trap
nano drosera.toml
```
Add the following codes at the bottom of `drosera.toml`:
```toml
private_trap = true
whitelist = ["Operator_Address"]
```
* Replace `Operator_Address` with your EVM wallet `Public Address` between " " symbols
* Your `Public Address` is your `Operator_Address`.

**2- Update Trap Configuration:**
```bash
DROSERA_PRIVATE_KEY=xxx drosera apply
```
* Replace `xxx` with your EVM wallet `privatekey`
IF found error wait a minutes, because cooldown
![image](https://github.com/user-attachments/assets/49fccc1c-7a25-4b63-bc3d-0daf47c4c04f)

Your Trap should be private now with your operator address whitelisted internally.

![image](https://github.com/user-attachments/assets/9ae6d58e-3be7-4d0d-9c4b-3b486224df4e)

---

## 2. Install Operator CLI
```bash
cd ~
```
```bash
# Download
curl -LO https://github.com/drosera-network/releases/releases/download/v1.16.2/drosera-operator-v1.16.2-x86_64-unknown-linux-gnu.tar.gz

# Install
tar -xvf drosera-operator-v1.16.2-x86_64-unknown-linux-gnu.tar.gz
```
Test the CLI with `./drosera-operator --version` to verify it's working.
```console
# Check version
./drosera-operator --version

# Move path to run it globally
sudo cp drosera-operator /usr/bin

# Check if it is working
drosera-operator
```
## 3. Run Node
```bash
drosera-operator node \
  --db-file-path "$HOME/.drosera.db" \
  --network-p2p-port 31313 \
  --server-port 31314 \
  --eth-rpc-url https://ethereum-holesky-rpc.publicnode.com \
  --eth-backup-rpc-url https://1rpc.io/holesky \
  --drosera-address 0xea08f7d533C2b9A62F40D5326214f39a8E3A32F8 \
  --eth-private-key PV_KEY \
  --listen-address 127.0.0.1 \
  --network-external-p2p-address 127.0.0.1 \
  --disable-dnr-confirmation true

```
 Replace `PV_KEY` with your EVM wallet `privatekey`
## 8. Check Node Health

![image](https://github.com/user-attachments/assets/a4ad6e66-4749-4780-9347-c878399d4067)

**!! No problem if you are receiveing `WARN drosera_services::network::service: Failed to gossip message: InsufficientPeers`**

---
---

## 9. Opt-in Trap
In the dashboard., Click on `Opti in` to connect your operator to the Trap

![image](https://github.com/user-attachments/assets/5189b5cb-cb46-4d10-938a-33f71951dfc2)

---

## 10. Check Node Liveness
Your node will start producing greeen blocks in the dashboard

![image](https://github.com/user-attachments/assets/9ad08265-0ea4-49f7-85e5-316677245254)

