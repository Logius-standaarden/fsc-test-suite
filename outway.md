# Overview

| TestID                  | FSC                 | Description                                                                                 |
|-------------------------|---------------------|---------------------------------------------------------------------------------------------|
| Outway-TransactionLog-1 | Logging             | Create a TransactionLog record for a received request                                       |
| Outway-TransactionLog-2 | Logging             | Add a TransactionID                                                                         |
| Outway-TransactionLog-3 | Logging, Delegation | Create a TransactionLog record for a request made on behalf of another Peer                 |
| Outway-TransactionLog-4 | Logging, Delegation | Create a TransactionLog record for a request to a Service offered on behalf of another Peer |


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
