Overview

This document includes requirements and design details for developers to understand how a pre-fork, onchain exchange (ONX) may be implemented. The features described here are completely optional addons to forking. They enable an onchain exchange between post-fork coins before a fork. This means the market has immediate liquidity and a reliable price discovery mechanism for the fork. Liquidity and price discovery tools massively increase demand and price stability and provide important signals for all participants as they indicate verifiable demand for the fork. The onchain exchange can be achieved with standard transactions and with only a very small risk of anybody losing coins.  Before the hard fork split event there exists one chain, the current bitcoin blockchain herein labeled BSC0 (BlockStream Chain). Post fork there will be two chains BSC1 and BUC0 (Bitcoin Unlimited Chain).

Exchange process
Phase 1 - Making orders

Before the fork the first BUC0 clients will be released and the fork block will be known with enough time before the fork event to support onchain exchange features. Users who want to support the exchange need to download the BUC0 nodes with ONX features. Users who want to exchange need to download ONX clients. The ONX nodes and clients will include user features for the exchange such as a bid/offer list, buy/sell buttons and order status details. Users who want to make bids and offers will broadcast standard transactions to start the process for an exchange. These ONX transactions are used by the ONX nodes to build an order list with statuses. This drives the ONX client interface to assist the users with the exchange process. When the right transactions are broadcast the exchange process continues to settlement or cancellation as instructed by users.

As described in the following section, orders for BUC0 coins involve 2 steps for the maker and 2 steps for the taker (make, take, make, take). With automatic signing enabled these can be reduced to 1 step each (make, take) if users keep their clients online. In order to successfully finalize these orders users are advised to complete all these steps before the final orders block which is 30 blocks before the fork block.

In the background BUC0 ONX nodes will be building and maintaining a valid order list out of the blockchain data. These background tasks continue all the way until the fork block.  This gives time for ONX nodes to prepare for the settlement phase. 

Phase 2 - Settlement

After the final order block there are no further user steps necessary. After the fork block settlement is processed autonomously by the BUC0 nodes. Valid settlement transactions need exclusive mining priority to prevent double spend attacks but no other special tasks are required. After processing all orders, the onchain exchange is shutdown at the stop block which is 30 blocks after the fork block. The temporary rules enforcing high priority for valid settlement transactions are terminated. There are also some clean up tasks that are possible which prune all UTXOs that contain the bid and offer data.

