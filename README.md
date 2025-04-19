# kozel Wallet Balance Scanner

A Python script to scan a list of Ethereum wallet addresses, fetch their native balance via JSON-RPC, and categorize them into:

- **Empty Wallets**: Addresses with zero or unreachable balances saved to `empty.txt`.
- **Rich Wallets**: Addresses with balances greater than 0.1 ETH saved (with full details) to `with_balance.json`, sorted from highest to lowest balance.

This tool is ideal for auditing large batches of addresses for faucets, airdrops, or balance tracking.

---

## Features

- **Fast Processing**: Uses `tqdm` for a progress bar when iterating through addresses.
- **JSON-RPC Compatibility**: Works with any Ethereum-compatible JSON-RPC endpoint (e.g., Infura, Alchemy, or a self‑hosted node).
- **Balance Thresholding**: Easily adjust the minimum balance threshold (default: 0.1 ETH) to classify "rich" wallets.
- **Sorted Output**: Rich wallets are output in descending order by balance for quick inspection.

## Prerequisites

- Python 3.7 or higher
- `requests` library
- `tqdm` library

Install dependencies via pip:

```bash
pip install requests tqdm
```

## Configuration

1. **RPC Endpoint**: Edit the `RPC_ENDPOINT` constant at the top of the script to point to your Ethereum JSON-RPC provider:
   ```python
   RPC_ENDPOINT = "https://your-provider.io/v3/YOUR_API_KEY"
   ```

2. **Input File**: Place your wallet list in `wallets.json`. The file should be an array of objects with at least `address` and `privateKey` fields:
   ```json
   [
     {
       "address": "0xAbc...",
       "privateKey": "0x123..."
     },
     {
       "address": "0xDef...",
       "privateKey": "0x456..."
     }
   ]
   ```

## Usage

Run the script from a terminal:

```bash
python3 balancer.py
```

Upon completion, you will find:

- `empty.txt`: A newline-separated list of addresses with zero balance or fetch errors.
- `with_balance.json`: A JSON array of wallet objects (including `address`, `privateKey`, and `balance`) for addresses with > 0.1 ETH, sorted high-to-low.

## Customization

- **Balance Threshold**: Change the `0.1` value in:
  ```python
  if balance is not None and balance > 0.1:
  ```
  to any other Ether value to adjust what counts as a "rich" wallet.

- **Output Filenames**: Modify the filenames `empty.txt` and `with_balance.json` in the save sections.

## License

This project is released under the **MIT License**. See [LICENSE](LICENSE) for details.


