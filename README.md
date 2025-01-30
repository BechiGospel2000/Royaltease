# Royaltease Smart Contract  

## Overview  
**Royaltease** is an automated royalty distribution smart contract built on Clarity. It enables creators to register their works, define royalty rates, and distribute earnings to stakeholders in a decentralized, transparent, and efficient manner. The contract ensures fair revenue sharing among contributors and automates the withdrawal of earnings.

## Features  
- **Work Registration**: Creators can register their intellectual property with a defined royalty rate.  
- **Stakeholder Management**: Creators can add stakeholders and allocate shares.  
- **Automated Royalty Distribution**: Earnings are automatically split and assigned to stakeholders.  
- **Secure Withdrawals**: Stakeholders can withdraw their earnings securely.  
- **Transparency & Fairness**: Enforces share limits and ensures proper fund allocation.  

## Error Codes  
| Error Code | Description |
|------------|------------|
| `u100` | Not Authorized |
| `u101` | Invalid Work |
| `u102` | Invalid Stakeholder |
| `u103` | Invalid Share |
| `u104` | Shares Exceed 100% |
| `u105` | Insufficient Funds |
| `u106` | Transfer Failed |

## Contract Components  

### 1. **Data Structures**  
- **`works`**: Stores registered works with creator, title, royalty rate, and earnings.  
- **`work-stakeholders`**: Maps stakeholders to their respective shares in a work.  
- **`earnings`**: Tracks the earnings available for withdrawal by each stakeholder.  

### 2. **Public Functions**  
- `register-work (title, royalty-rate)`: Registers a new work under the sender’s account.  
- `add-stakeholder (work-id, stakeholder, share)`: Assigns a share of earnings to a stakeholder.  
- `distribute-royalty (work-id, amount)`: Distributes royalty revenue among stakeholders.  
- `withdraw-earnings ()`: Allows stakeholders to withdraw their earnings.  

### 3. **Read-Only Functions**  
- `get-work-details (work-id)`: Retrieves details of a registered work.  
- `get-stakeholder-share (work-id, stakeholder)`: Gets a stakeholder’s share for a work.  
- `get-earnings (account)`: Checks an account’s available earnings.  

### 4. **Private Functions**  
- `distribute-to-stakeholders (work-id, amount)`: Handles the distribution of earnings.  
- `get-total-share (work-id)`: Calculates total allocated shares for a work.  
- `get-stakeholders (work-id)`: Retrieves stakeholders for a work.  

## Usage  
1. **Register a Work**  
   ```clarity
   (register-work "My Song" u10)
   ```
   - Registers "My Song" with a 10% royalty rate.  

2. **Add a Stakeholder**  
   ```clarity
   (add-stakeholder u0 'SP1234ABCD' u30)
   ```
   - Assigns a 30% share to `SP1234ABCD` for work ID `0`.  

3. **Distribute Royalties**  
   ```clarity
   (distribute-royalty u0 u1000)
   ```
   - Distributes 10% of `1000` STX among stakeholders of work `0`.  

4. **Withdraw Earnings**  
   ```clarity
   (withdraw-earnings)
   ```
   - Transfers available earnings to the caller’s wallet.  

## Security Considerations  
- Only the creator of a work can manage stakeholders.  
- Total allocated shares cannot exceed 100%.  
- Ensures sufficient contract balance before distribution.  
- Withdrawals are only permitted if earnings are available.  

## License  
This smart contract is open-source and licensed under the MIT License.  