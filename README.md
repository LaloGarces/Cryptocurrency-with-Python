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

 ```
app.run(host='0.0.0.0', port=5000)
app.run(host='0.0.0.0', port=5001)
app.run(host='0.0.0.0', port=5003)

 ```
