# Overview

| TestID                   | FSC                 | Description                                                                                 |
|--------------------------|---------------------|---------------------------------------------------------------------------------------------|
| Outway-IncomingRequest-1 | Core                | Receive a request that can be proxied to the Inway                                          |
| Outway-IncomingRequest-2 | Core                | Receive a request that cannot be proxied to the Inway                                       |
| Outway-IncomingRequest-3 | Core                | Receive a request that is proxied to a failing Inway                                        |
| Outway-TransactionLog-1  | Logging             | Create a TransactionLog record for a received request                                       |
| Outway-TransactionLog-2  | Logging             | Add a TransactionID                                                                         |
| Outway-TransactionLog-3  | Logging, Delegation | Create a TransactionLog record for a request made on behalf of another Peer                 |
| Outway-TransactionLog-4  | Logging, Delegation | Create a TransactionLog record for a request to a Service offered on behalf of another Peer |
| Outway-TransactionLog-5  | Logging | An error occured while writing to the TransactionLog                                        |

# Outway-IncomingRequest-1

Scenario: The Outway receives a request and is able to proxy this request to the Inway providing the service
Given a valid contract with a ServiceConnectionGrant for the Peer exists
When a request is received the outway is able to obtain a valid accessToken based on the ServiceConnectionGrant
Then the request is sent to the Inway and the response from the Inway is received by the Outway

# Outway-IncomingRequest-2

Scenario: The Outway receives a request and is unable to obtain a valid access token
Given a valid contract with a ServiceConnectionGrant for the Peer does not exist
When a request is received the outway is not able to obtain a valid accessToken based on the ServiceConnectionGrant
Then the request is not sent to the Inway, the Outway returns an error

# Outway-IncomingRequest-3

Scenario: The Outway receives a request and is unable to reach the Inway
Given a valid contract with a ServiceConnectionGrant for the Peer exist
When a request is received the outway is able to obtain a valid accessToken based on the ServiceConnectionGrant
Then the request is sent to the Inway who is unreachable, the Outway returns an error

# Outway-TransactionLog-1

Scenario: Create a TransactionLog record for a received request
Given a valid Contract with a ServiceConnectionGrant for the Peer exists
When a request for with a Grant Hash is received
Then the Outway should write a TransactionLog for the request before sending the request to the Inway

# Outway-TransactionLog-2

Scenario: Add a TransactionID
Given a Contract containing a ServiceConnectionGrant for the Peer exists
When the Outway sends the request to the Inway
Then the TransactionLog ID should be present in the request to the Inway

# Outway-TransactionLog-3

Scenario: Create a TransactionLog record for a request made on behalf of another Peer
Given a Contract containing a DelegatedServiceConnectionGrant for the Peer exists
When a request with a Grant Hash is received
Then the Outway should write a TransactionLog for the request in which the source contains the Delegator

# Outway-TransactionLog-4

Scenario: Create a TransactionLog record for a request made on behalf of another Peer
Given the Service is being offered on behalf of another Peer
And a valid Contract with a ServiceConnectionGrant for the Peer exists
When a request with a Grant Hash is received
Then the Outway should write a TransactionLog for the request in which the destination contains the Delegator

# Outway-TransactionLog-5

Scenario: An error occurs while writing to the transaction log
Given the transaction log is not in working order
When a request is received
Then the Outway should try to write to the transaction log and upon receiving an error from the transaction log the Outway must respond with an error and not proxy the request to the Inway
