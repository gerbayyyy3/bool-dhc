# Bool Network DHC Node Setup

## 1. DHC Node Setup

Install Dependencies
```
# Update system and install dependencies
sudo apt update && sudo apt upgrade -y
sudo apt install build-essential cmake pkg-config libssl-dev -y
```
Install Rust & Set Up Environment
```
# Install Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
rustup update stable
```
Clone the Repository
```
# Clone DHC node repository
git clone https://github.com/boolnetwork/dhc-node.git
cd dhc-node
cargo build --release
```
Start the Node
```
# Run the node (connects to beta testnet)
./target/release/dhc-node --chain testnet --name "YourNodeName"
```

## 2. Local LAN Configuration for SGX

Install Intel SGX Drivers
```
# Download and install SGX driver
wget https://download.01.org/intel-sgx/latest/linux-latest/distro/ubuntu20.04-server/sgx_linux_x64_driver_2.11.0_eb.tar.gz
tar -xvf sgx_linux_x64_driver_2.11.0_eb.tar.gz
cd sgx_linux_x64_driver
sudo make
sudo make install
Enable SGX in BIOS
```
Restart the machine.
Go to BIOS → Advanced Settings → Enable Intel SGX.
Verify SGX Installation
```
# Check if SGX is enabled
dmesg | grep SGX
```

## 3. Run a Chain via Snapshot

Download Snapshot
```
# Download snapshot
wget https://bool.network/snapshots/testnet/snapshot.tar.gz
tar -xvzf snapshot.tar.gz -C $HOME/.dhc
```
Start Node from Snapshot
```
# Start node using snapshot
./target/release/dhc-node --chain testnet --base-path $HOME/.dhc --name "YourNodeName"
```
## 4. Case Study: Validator Node

Create a Validator Account
```
# Generate new account
./target/release/dhc-key generate
```
Start Validator Node
```
# Start node as validator
./target/release/dhc-node --validator --name "YourValidatorNode"
```
Stake Tokens
Use the Bool Network dashboard to stake tokens in your validator.
