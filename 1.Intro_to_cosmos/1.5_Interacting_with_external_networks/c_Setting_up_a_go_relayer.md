## How to Setup a Go Relayer Between 2 Cosmos Chains

Setting up a Go relayer between two Cosmos chains involves a few steps. Here is a high-level overview of the process:

1.  Install the Go programming language and the Relayer package. You can find installation instructions for both on their respective websites.
    
2.  Create a configuration file for each of the chains you want to relay. This file should include the chain's ID, its RPC endpoint, and any other relevant information. You can find examples of configuration files in the Relayer documentation.
    
3.  Initialize the relayer by running the following command: 
    
    `rly init` 
    
    This will create a directory structure for the relayer and generate a configuration file for it.

4.  Add the two chains to the relayer by running the following commands: 
   `rly chains add -f <path-to-config-file-1>`
   
    `rly chains add -f <path-to-config-file-2>`

    `rly keys add <chain1> user1`
    
    `rly keys add <chain2> user2`
 
    
    This will register the two chains with the relayer and enable it to communicate with them.

5.  Create a connection between the two chains by running the following commands: 
    
    `rly paths generate <src-chain-id> <dst-chain-id> <path-name>`

    `rly paths show <path-name>`  

    The first command will generate a path between the two chains, and the second command will display the path details.

6.  Finally, start the relayer by running the following command: 

    `rly start <path-name>` 

    This will start the relayer and begin relaying packets between the two chains.