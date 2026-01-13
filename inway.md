# Overview

| TestID                   | FSC                 | Description                                                                                 |
|--------------------------|---------------------|---------------------------------------------------------------------------------------------|
| Inway-Incoming-Request-1 | Core                | Receive a request with a valid access token                                                 |
| Inway-Incoming-Request-2 | Core                | Receive a request without an access token                                                   |
| Inway-Incoming-Request-3 | Core                | Receive a request with an access token bound to a different certificate                     |
| Inway-Incoming-Request-4 | Core                | Receive a request with an untrusted certificate                                             |
| Inway-Incoming-Request-5 | Core                | Preserve access token                                                                       | 
| Inway-Incoming-Request-6 | Core                | Receive a request with an expired access token                                              | 
| Inway-TransactionLog-1   | Logging             | Create a TransactionLog record for a received request                                       |
| Inway-TransactionLog-2   | Logging             | Preserve TransactionID                                                                      |
| Inway-TransactionLog-3   | Logging             | Reject request without a TransactionID                                                      |
| Inway-TransactionLog-4   | Logging             | Create a TransactionLog record for a request made on behalf of another Peer                 |
| Inway-TransactionLog-5   | Logging             | Create a TransactionLog record for a request to a Service offered on behalf of another Peer |
| Inway-TransactionLog-6   | Logging             | An error occurred while writing to the transaction log                                      |
| Inway-Port-1             | Core                | Accept request on port 443 or 8443                                                          |


# Inway-Incoming-Request-1

Scenario: Receive a request with a valid access token
When a request with a valid access token is received
Then the request should be accepted

# Inway-Incoming-Request-2

Scenario: Receive a request without an access token
When a request without an access token is received
Then the request should be denied

# Inway-Incoming-Request-3

Scenario: Receive a request with an access token bound to a different certificate
When a request an access token is received
And the certificate of the incoming connection does not match the certificate defined in the access token
Then the request should be denied

# Inway-Incoming-Request-4

Scenario: Receive a request with an untrusted certificate
When a request is received
And the certificate of the incoming connection is not signed by the Trust Anchor of the Group
Then the request should be denied

# Inway-Incoming-Request-5

Scenario: Preserve access token 
When a request with a valid access token is received
Then the access token should be received by the Service

# Inway-Incoming-Request-6

Scenario: Receive a request with an expired access token
When a request is with an expired access token received
Then the request should be denied

# Inway-TransactionLog-1

Scenario: Create a TransactionLog record for a received request
When a request with a valid access token is received
Then the Inway should write a TransactionLog for the request before proxying the request to the Service

# Inway-TransactionLog-2

Scenario: Preserve TransactionID
When a request with a valid access token is received
Then the TransactionLog ID should be present in the request to the Service

# Inway-TransactionLog-3

Scenario: Reject request without a TransactionID
When a request with a valid access token is received
And no TransactionID is present in the request
Then the Inway should reject the request 

# Inway-TransactionLog-4

Scenario: Create a TransactionLog record for a request made on behalf of another Peer
Given the Service connection is allowed because of a Contract containing a DelegatedServiceConnectionGrant
When a request with a valid access token is received
Then the Inway should write a TransactionLog for the request in which the source contains the Delegator

# Inway-TransactionLog-5

Scenario: Create a TransactionLog record for a request made on behalf of another Peer
Given the Service is being offered on behalf of another Peer
When a request with a valid access token is received
Then the Inway should write a TransactionLog for the request in which the destination contains the Delegator

# Inway-TransactionLog-6

Scenario: An error occurs while writing to the transaction log
Given the transaction log is not in working order
When a request with a valid access token is received
Then the Inway should try to write to the transaction log and upon receiving an error from the transaction log the Inway must respond with an error and not invoke the Service

# Inway-Port-1

Scenario: Accept request on port 443 or 8443
When a request is sent to either port 443 or 8443
Then the Inway should respond
