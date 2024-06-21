# ParticleNetwork

[![Telegram channel](https://img.shields.io/endpoint?url=https://runkit.io/damiankrawczyk/telegram-badge/branches/master?url=https://t.me/oxcode1)](https://t.me/oxcode1)

✈️ [Telegram Channel](https://t.me/oxcode1)

![img1](data/demo/demo.png)

## 💡 Functionality
| Feature                                                          | Supported  |
|------------------------------------------------------------------|:----------:|
| Multithreading                                                   |     ✅     |
| Local database                                                   |     ✅     |
| Captcha support (CapMonster, Twocaptcha, AntiCaptcha)            |     ✅     |
| Proxy support (HTTP ONLY)                                        |     ✅     |
| Load list by REFCODE                                             |     ✅     |
| Support for all EVM networks                                     |     ✅     |
| Perform Daily CHECK-IN                                           |     ✅     |
| Perform DEPOSIT UNIVERSAL GAS                                    |     ✅     |
| Perform USE UNIVERSAL GAS TO TRANSACT (100 transactions/24h)     |     ✅     |
| Perform RETWEET PARTICLE NETWORK'S TWEET                         |     ✅     |
| Gather account and EVM wallet information                        |     ✅     |
| Export account information to txt, excel                         |     ✅     |
| Generate EVM wallets                                             |     ✅     |
| And more :)                                                      |     ✅     |

## [⚙️ Settings](https://github.com/NikeAK/ParticleNetwork/blob/main/data/config.py)
| Setting                   | Description (see config.py)                                                |
|---------------------------|-----------------------------------------------------------------------------|
| **MAIN_NETWORK**          | Choose the main network by specifying a number                             |
| **DEPOSIT_USDG**          | Specify numbers [min, max] for USDG deposit amount in your network         |
| **DEPOSIT_PARTICLE**      | Specify numbers [min, max] for ParticleWallet deposit amount in your network|
| **MAKE_TRANSACTIONS**     | Execute 100 transactions for the daily task?                               |
| **MAX_GAS_USDG**          | Maximum USDG gas fee, varies significantly across networks.                |
| **TRANSFER_AMOUNT**       | Specify numbers [min, max] for transfer amount during transaction execution.|
| **DELAY_TRANSACTIONS**    | Specify numbers [min, max] for delay between transactions.                 |
| **RANDOM_TX**             | Enable random transactions?                                                |
| **TIMEOUT_PROXY**         | Maximum wait time when checking proxies in seconds                         |
| **REQUEST_ATTEMPTS**      | Number of attempts for unsuccessful requests                               |
| **CAPTCHA_API_KEY**       | Captcha key                                                                |
| **GET_ALL_BALANCES**      | Retrieve current balance of all EVM networks?                              |
| **DELAY_ALL_BALANCES**    | Delay in seconds between retrieving balance in 1 network/1 wallet          |
| **EXPORT_DATA**           | Data to be exported                                                        |
| **EXPORT_SEPARATOR**      | Data separator symbol for exporting to TXT                                 |

## 📝 Instructions
1. Fill in config.py
2. Load accounts into text files
3. On first launch, select Launch - Add account to database in the terminal
    - The software logs into the ParticleNetwork account and checks if the referral code is set. If not, it assigns the code to the account. It then checks if Twitter is linked. If it is, it skips Twitter linking; if not, it takes a token from the file, verifies it, and links it to the account. The account is then added to the database.
    - Do not press CTRL+C during this process, as data will be removed from the TXT file and it’s not guaranteed that it was added to the database or that Discord/Twitter was linked to an account. Re-uploading the accounts won’t necessarily fix this as the software does not check if Twitter/Discord accounts are linked to another account, which may lead to errors later.
4. After successfully adding accounts, you can choose Launch -> DataBase in the terminal
    - The software simply performs tasks and executes transactions. After successful completion, it updates the account and wallet information/statistics (if GET_ALL_BALANCES is enabled).
    - Note that for the USE UNIVERSAL GAS TO TRANSACT task, the software withdraws small amounts from Particle Wallet to your main EVM wallet. If the Particle Wallet balance is insufficient, it performs a DEPOSIT_PARTICLE operation. The same process applies for USDG gas fees.
    - You can set the maximum gas fee for USDG transactions. I didn’t add a maximum gas fee for EVM wallets, but you can regulate it with MULTIPLIER_GAS.
    - To avoid sending transactions only from ParticleWallet, you can enable random transactions. The software generates a random number from 1 to 12. If it’s 1, it makes an additional DEPOSIT_PARTICLE transaction. If it’s 12, it makes an additional DEPOSIT_USDG transaction.
5. After going through the entire database, you can export all available information.
    - You will be prompted to choose which information to export: by default, config.py is used (see config.py), or you can choose the required information using the arrow keys. Then select the export format: TXT or Excel.
6. Repeat step 4 daily and wait for profit, as the testnet is expected to be rewarded :)

## ⚡️ Quick Start
1. Run $\color{orange}{\textsf{Setup.bat}}$. This script will automatically create a virtual environment, activate it, install all necessary dependencies from the requirements.txt file, and remove unnecessary files.
2. After successfully running $\color{orange}{\textsf{Setup.bat}}$, you can launch $\color{orange}{\textsf{Main.bat}}$. This script will activate the virtual environment and start the software.

## 🛠️ Manual Installation
```shell
~ >>> python -m venv Venv              # Create a virtual environment
~ >>> Venv/Scripts/activate            # Activate the virtual environment
~ >>> pip install -r requirements.txt  # Install dependencies
~ >>> python main.py                   # Run the software
