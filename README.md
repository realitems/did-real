# Real Items DID Method Specification

V0.1

## DID Scheme

Real Items DIDs are identifiable by the DID method `real`.

A Real Items DID has the following format:

```did:real:<Ethereum address>```

For example:

```did:real:0x70997970C51812dc3A010C7d01b50e0d17dc79C8```

## Method Operations

Real Items DIDs are managed via the Real Items DID registry smart contract.

### Create

To create a DID, submit a transaction to the registry contract invoking the `createDid` method.

This will generate a DID document on-chain, where the DID subject is the Ethereum address of the transaction sender.

### Resolve

DID documents can be looked up by invoking the `resolveDidDocument` method of the registry contract.

To ensure the smart contract invocation result is trustworthy, the client could query a certain number of nodes and then compare the return values.

```json
{
  "@context": "https://www.w3.org/ns/did/v1",
  "id": "did:real:0x70997970C51812dc3A010C7d01b50e0d17dc79C8",
  "verificationMethod": [
	{
	  "id": "did:real:0x70997970C51812dc3A010C7d01b50e0d17dc79C8#key-1",
	  "type": "EcdsaSecp256k1RecoveryMethod2020",
	  "controller": "did:real:0x70997970C51812dc3A010C7d01b50e0d17dc79C8",
	  "blockchainAccountId": "eip155:1:0x70997970C51812dc3A010C7d01b50e0d17dc79C8"
	}
  ]
}
```

### Update

Updating the DID is not possible.

### Deactivate

Only the controller address is able to deactivate an active DID. To deactivate a DID, submit a transaction to the registry contract invoking the `deactivateDid` method.

A deactivated DID cannot be reactivated.

## Security Considerations

- The entity that controls the private key which controls the DID effectively controls the DID document. Proper care should be taken to ensure that the private key is kept secure. Key recovery methods which applies to Ethereum keys apply here. Methods for ensuring key privacy are outside the scope of this document.

## Privacy Considerations

- This DID method only stores Ethereum addresses. There are no privacy concerns implicit to the method. However, care must be taken when using a single DID for several purposes if correlation is undesired.
