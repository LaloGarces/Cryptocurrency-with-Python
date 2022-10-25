# Cryptocurrency Transactions Demo with Python

## This project was developed with the intention to be used like Demo and understand in a better way, how Blockchain, Nodes, Crypto mining and Transactions in the Blockchain works, in a decentralized way.

### We're going to use Colab for the development of the code in Python and Postman to get some request we're going to send from Colab with Flask and play with the demo. This demo is perfect to teach students how Cryptocurrency Transactions works. 

- For more information about Postman: https://www.postman.com/
- For more information about Flask: https://flask.palletsprojects.com/en/2.2.x/

### The project is divided in the next sections:  

1. Importing libraries.
2. Creating the Blockchain and the Cryptocurrency.
3. Mining the Blockchain.
4. Decentralizing the Blockchain.
5. Running the demo with Flask and Postman.

### Important. 

After running the Code and when running the Demo, it is important to put attention in the next steps to run correctly the Demo:

### Step 1

Important to run the code of each node in different computers or terminals to create a decentralized blockchain and send transactions to each computer/node.

How can we run different nodes with the same code?

Simple, just at the moment to run the Demo, for each node, just you need to change the port. In the case if this demo, we used 3 different ports/nodes, but you can use as many as you like. 

- port=5000 (Computer 1)
- port=5001 (Computer 2)
- port=5002 (Computer 3)

 ```
app.run(host='0.0.0.0', port=5000)
app.run(host='0.0.0.0', port=5001)
app.run(host='0.0.0.0', port=5003)
 ```
 
 Create the genesis block with the port 5000 (Node 1) and the GET: get_chain:

 ```
 {
    "chain": [
        {
            "index": 1,
            "previous_hash": "0",
            "proof": 1,
            "timestamp": "2022-10-25 14:26:36.240661",
            "transactions": []
        }
    ],
    "length": 1
}
 ``` 
 
 ## Step 2
 
Create genesis Block with port 5001 for the second computer/node and port 5002 for the third computer/node:

 Node 2
 ```
{
    "chain": [
        {
            "index": 1,
            "previous_hash": "0",
            "proof": 1,
            "timestamp": "2022-10-25 14:26:50.214574",
            "transactions": []
        }
    ],
    "length": 1
}
 ```
 
 Node 3
  ```
  {
    "chain": [
        {
            "index": 1,
            "previous_hash": "0",
            "proof": 1,
            "timestamp": "2022-10-25 14:27:00.446063",
            "transactions": []
        }
    ],
    "length": 1
}
   ```

 ## Step 3

Connect the nodes with the json file of "Nodes" & the connect_node.

Within postman please follow the next route: POST > Body > Raw > JSON.

Like we're connecting the nodes from node 1, we only in the JSON file use node 2 and node 3:

Input

```
{
    "nodes": ["http://127.0.0.1:5001",
              "http://127.0.0.1:5002"]
}
```

Output

```
{
    "message": "All nodes are now connected. The Altcoin Blockchain contains the following nodes:",
    "total_nodes": [
        "127.0.0.1:5001",
        "127.0.0.1:5002"
    ]
}
```
Do the same for the other 2 nodes. 

 ## Step 4
 
 In node 1 mine the block with mine_block. It's important to mine the Block to register the transaction done in the previous step. Notice that the amount sent was 1 Altcoin:
 
 ```
 {
    "index": 2,
    "message": "You just have mined succesfully a block!",
    "previous_hash": "0f4370ab93384b986c6d5d809c25e3b1296a6e894998d8d8c0d8a293ba380816",
    "proof": 533,
    "timestamp": "2022-10-25 14:49:09.542492",
    "transactions": [
        {
            "amount": 1,
            "receiver": "Lalo",
            "sender": "09e6204d064c4e408bbca133d94a66af"
        }
    ]
}
```

 ## Step 5
 
 In node 1, use the get_chain to se all the current blocks you have in your current chain:

```
 {
    "index": 2,
    "message": "You just have mined succesfully a block!",
    "previous_hash": "0f4370ab93384b986c6d5d809c25e3b1296a6e894998d8d8c0d8a293ba380816",
    "proof": 533,
    "timestamp": "2022-10-25 14:49:09.542492",
    "transactions": [
        {
            "amount": 1,
            "receiver": "Lalo",
            "sender": "09e6204d064c4e408bbca133d94a66af"
        }
    ]
}
```

## Step 6

If we ask to our nodes to verify their current chain, they're not going to have the largest chain. Only in their chain, they're going to have the genesis block:

```
http://0.0.0.0:5001/get_chain
```

```
{
    "chain": [
        {
            "index": 1,
            "previous_hash": "0",
            "proof": 1,
            "timestamp": "2022-10-25 14:43:42.913803",
            "transactions": []
        }
    ],
    "length": 1
}
```


```
http://0.0.0.0:5002/get_chain
```

```
{
    "chain": [
        {
            "index": 1,
            "previous_hash": "0",
            "proof": 1,
            "timestamp": "2022-10-25 14:43:47.005129",
            "transactions": []
        }
    ],
    "length": 1
}
```

## Step 7

Asking to each node use the replace_chain, is going to let us add the new blocks to each of the nodes:

```
http://0.0.0.0:5001/replace_chain
```

```
{
    "message": "The nodes had different chains so the chain was replaced by the longest one.",
    "new_chain": [
        {
            "index": 1,
            "previous_hash": "0",
            "proof": 1,
            "timestamp": "2022-10-25 14:43:38.026823",
            "transactions": []
        },
        {
            "index": 2,
            "previous_hash": "0f4370ab93384b986c6d5d809c25e3b1296a6e894998d8d8c0d8a293ba380816",
            "proof": 533,
            "timestamp": "2022-10-25 14:49:09.542492",
            "transactions": [
                {
                    "amount": 1,
                    "receiver": "Lalo",
                    "sender": "09e6204d064c4e408bbca133d94a66af"
                }
            ]
        }
    ]
}
```

```
http://0.0.0.0:5002/replace_chain
```

```
{
    "message": "The nodes had different chains so the chain was replaced by the longest one.",
    "new_chain": [
        {
            "index": 1,
            "previous_hash": "0",
            "proof": 1,
            "timestamp": "2022-10-25 14:43:38.026823",
            "transactions": []
        },
        {
            "index": 2,
            "previous_hash": "0f4370ab93384b986c6d5d809c25e3b1296a6e894998d8d8c0d8a293ba380816",
            "proof": 533,
            "timestamp": "2022-10-25 14:49:09.542492",
            "transactions": [
                {
                    "amount": 1,
                    "receiver": "Lalo",
                    "sender": "09e6204d064c4e408bbca133d94a66af"
                }
            ]
        }
    ]
}
```








