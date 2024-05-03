# Overview

| TestID                                  | FSC     | Description                                                                     |
|-----------------------------------------|---------|---------------------------------------------------------------------------------|
| Integration-ConsumeService-1            | Core    | Consume a Service                                                               |
| Integration-ConsumeService-2            | Core    | Consume a Service without a valid Contract                                      |
| Integration-ConsumeServiceAsDelegatee-1 | Core    | Consume a Service with a DelegatedServiceConnectionGrant                        |
| Integration-ConsumeDelegatedService-1   | Core    | Consume a Service with a ServiceConnectionGrant containing a Delegator          |
| Integration-ConsumeDelegatedService-2   | Core    | Consume a Service with a DelegatedServiceConnectionGrant containing a Delegator |
| Integration-TransactionLog-1            | Logging | Create TransactionLog records                                                   |


# Integration-ConsumeService-1

Scenario: Consume a Service
Given the Peer has a valid Contract with a ServiceConnectionGrant
When the Peer calls the Service using the Outway
Then the Service should return a successful response

# Integration-ConsumeService-2

Scenario: Consume a Service without a valid Contract
Given the Peer does not have a valid Contract with a ServiceConnectionGrant
When the Peer call the Service using the Outway
Then the Outway should reject the request

# Integration-ConsumeServiceAsDelegatee-1

Scenario: Consume a Service on behalf of another Peer 
Given the Peer has a valid Contract with a DelegatedServiceConnectionGrant
When the Peer calls the Service using the Outway
Then the Service should return a successful response

# Integration-ConsumeDelegatedService-1

Scenario: Consume a Service which is published by a Delegatee
Given the Service is published using a DelegatedServicePublicationGrant
Given the Peer has a valid Contract with a ServiceConnectionGrant
When the Peer calls the Service using the Outway
Then the Service should return a successful response

# Integration-ConsumeDelegatedService-2

Scenario: Consume a Service on behalf of another Peer which is published by a Delegatee
Given the Service is published using a DelegatedServicePublicationGrant
Given the Peer has a valid Contract with a DelegatedServiceConnectionGrant
When the Peer calls the Service using the Outway
Then the Service should return a successful response

# Integration-Transaction-1

Scenario: Create TransactionLog records
Given a Peer has a valid Contract with a ServiceConnectionGrant
When the Peer calls the Service using the Outway
Then the consuming Peer should have created a TransactionLog record
And the providing Peer should have created a TransactionLog record
And the TransactionID of the TransactionLog records should match 
