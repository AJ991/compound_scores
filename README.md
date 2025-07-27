# Overview

The Compound Transaction Analyzer is a Python script (compound_transaction_analyzer.py) designed to process transaction data from Compound V2 and other DeFi protocols, feature engineer a comprehensive set of metrics based on 203 transaction types, and calculate a credit score for each wallet. The credit score (0–1000, where 0 indicates high risk and 1000 indicates low risk) is based on features like deposits, borrows, repayments, liquidations, and DeFi interactions. The output is a CSV file (compound_wallet_stats.csv) containing only the wallet address and credit score for each wallet.

The script processes an 800MB JSON file (compound_transactions.json) containing transaction data for over 100 wallets, fetched using a separate script (e.g., fetch_compound_transactions.py with the Covalent API). It handles a wide range of transaction types, including Compound V2 events (e.g., Mint, Borrow, RepayBorrow), collateral management events (e.g., Deposit, Withdraw), and other DeFi activities (e.g., Swap, FlashLoan).
--

# Features

Feature Engineering: Extracts 20 features from 203 transaction types, including:

Monetary metrics: total_deposit_usd, total_borrow_usd, total_repay_usd, total_redeem_usd, total_comp_received.

Count-based metrics: num_deposits, num_borrows, num_repays, num_redeems, num_liquidations, num_transfers, compound_core_tx_count, compound_reward_tx_count, interest_event_count, collateral_management_count, defi_interaction_count, token_interaction_count, staking_voting_count, defi_diversity_score.

Ratio-based metrics: avg_borrow_per_tx, avg_repay_per_tx, debt_to_collateral_ratio, liquidation_to_tx_ratio, compound_core_tx_ratio, collateral_to_borrow_ratio.

Credit Scoring: Calculates a weighted credit score (0–1000) based on normalized features, rewarding safe behaviors (e.g., deposits, repayments) and penalizing risky ones (e.g., liquidations, high debt).

Output: Generates compound_wallet_stats.csv with only wallet_address and credit_score for each wallet.

Large Data Handling: Processes an 800MB JSON file, with recommendations for memory optimization using ijson if needed.
