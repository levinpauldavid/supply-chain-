# Aim:
To develop a smart contract that tracks the supply chain of luxury goods, ensuring authenticity.
# Algorithm:
Step 1 : The manufacturer records product creation details on-chain.


Step 2 : The product moves through different supply chain checkpoints.


Step 3 : The ownership of the product can be transferred securely.


Step 4 : Buyers can verify the product’s authenticity.


# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LuxurySupplyChain {
    struct Product {
        string name;
        address currentOwner;
        bool verified;
    }

    mapping(uint256 => Product) public products;

    event ProductRegistered(uint256 productId, string name);
    event OwnershipTransferred(uint256 productId, address newOwner);

    function registerProduct(uint256 productId, string memory name) public {
        require(products[productId].currentOwner == address(0), "Product already registered");
        products[productId] = Product(name, msg.sender, true);
        emit ProductRegistered(productId, name);
    }

    function transferOwnership(uint256 productId, address newOwner) public {
        require(products[productId].currentOwner == msg.sender, "Not the owner");
        products[productId].currentOwner = newOwner;
        emit OwnershipTransferred(productId, newOwner);
    }

    function verifyProduct(uint256 productId) public view returns (string memory, address, bool) {
        Product memory p = products[productId];
        return (p.name, p.currentOwner, p.verified);
    }
}
```
# Expected Output:
A luxury good (e.g., a Rolex watch) is registered on-chain.


Ownership is transferred at every checkpoint.


Buyers can check the authenticity before purchasing.


# High-Level Overview:
Helps prevent counterfeit luxury goods.


Teaches real-world supply chain use cases.

# RESULT : 
TRANSACTION

![image](https://github.com/user-attachments/assets/98230a3e-0048-4e4a-9c9e-918a7e47596a)
![image](https://github.com/user-attachments/assets/49c709cf-a12a-43d8-8b06-ae31acf84532)
![image](https://github.com/user-attachments/assets/2367b899-6a70-4fbf-a3e6-26dd7e704688)

REGISTER PRODUCT

![image](https://github.com/user-attachments/assets/e4701e5f-2488-4700-8bec-f2f84590d46c)
![image](https://github.com/user-attachments/assets/0cf93325-5039-4cd2-b10e-3429db73f14b)

TRANSFER OWNERSHIP

![image](https://github.com/user-attachments/assets/460220f2-58e4-4c59-9670-836bfc83556d)
![image](https://github.com/user-attachments/assets/86abac4d-0720-49e9-92f9-987ad7f288a4)

PRODUCTS

![image](https://github.com/user-attachments/assets/bfd1f5f9-ee8f-4788-973a-8521330fba3f)
![image](https://github.com/user-attachments/assets/a0b1202c-94e2-4617-b3d9-9ccc2def465d)

VERIFY PRODUCT
![image](https://github.com/user-attachments/assets/ce133b7f-3342-4ad1-bef0-74be465f79b1)
![image](https://github.com/user-attachments/assets/98bb6c81-cc34-4b41-a762-de5cc7812ded)
