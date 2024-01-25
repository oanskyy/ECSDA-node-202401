## ECDSA Node

This project is an example of using a client and server to facilitate transfers between different addresses. Since there is just a single server on the back-end handling transfers, this is clearly very centralized. We won't worry about distributed consensus for this project.

However, something that we would like to incoporate is Public Key Cryptography. By using Elliptic Curve Digital Signatures we can make it so the server only allows transfers that have been signed for by the person who owns the associated address.

 
### Client

The client folder contains a [react app](https://reactjs.org/) using [vite](https://vitejs.dev/). To get started, follow these steps:

1. Open up a terminal in the `/client` folder
2. Run `npm install` to install all the depedencies
3. Run `npm run dev` to start the application 
4. Now you should be able to visit the app at http://127.0.0.1:5173/

### Server

The server folder contains a node.js server using [express](https://expressjs.com/). To run the server, follow these steps:

1. Open a terminal within the `/server` folder 
2. Run `npm install` to install all the depedencies 
3. Run `node index` to start the server 

The application should connect to the default server port (3042) automatically! 

_Hint_ - Use [nodemon](https://www.npmjs.com/package/nodemon) instead of `node` to automatically restart the server on any changes.


### Notes 

<!-- 1. to generate a private key
1. private key to generate an address(How to create a Bitcoin wallet address from a private key)  -->
2. Generating a private key is only a first step. 
3. The next step is extracting a public key and a wallet address that you can use to receive payments. The process of generating a wallet differs for Bitcoin and Ethereum,

Conclusion (Ethereum wallet address)
As you can see, creating an address for Ethereum is much simpler than for Bitcoin. All we need to do is to apply the ECDSA to public key, then apply Keccak-256, and finally take the last 20 bytes of that hash.

To create an Ethereum address, we need a public key which is derived from a private key.
!!!
Private keys can derive public keys and hence public keys can derive Ethereum addresses but the same cannot be said for vice-versa as it is not possible to derive public keys from Ethereum addresses and private keys from public keys.


Method 1: Using Elliptic Curve Digital Signature Algorithm (ECDSA).

Ethereum uses the secp256k1 curve. This is the special feature of ECDSA that we can derive the public key from the private key. We need to apply ECDSA to our private key to get the 64-byte integer in which the first 32 integers represent X and the other 32 integers represent Y on the elliptic curve.  

Conclusion (Bitcoin wallet address)
The wallet key generation process can be split into four steps:

1. creating a public key with ECDSA
2. encrypting the key with SHA-256 and RIPEMD-160
3. calculating the checksum with double SHA-256
4. encoding the key with Base58.
Depending on the form of public key (full or compressed), we get different addresses, but both are perfectly valid.

---

Elliptic Curve Digital Signature Algorithm (ECDSA): Key to Security

The ECDSA is explained as the fundamental method for signing Ethereum transactions.