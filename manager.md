# Overview

| TestID                         | RFC        | Description                                                                                               |
|--------------------------------|------------|-----------------------------------------------------------------------------------------------------------|
| Manager-SubmitContract-1       | Core       | Submit a Contract                                                                                         |
| Manager-SubmitContract-2       | Core       | Submit a Contract without being a Peer on the Contract                                                    |
| Manager-SubmitContract-3       | Core       | Submit a Contract with a PeerPublicationGrant                                                             |
| Manager-SubmitContract-4       | Core       | Submit a Contract with a ServicePublicationGrant                                                          |
| Manager-SubmitContract-5       | Delegation | Submit a Contract with a DelegatedServicePublicationGrant                                                 |
| Manager-SubmitContract-6       | Delegation | Submit a Contract with a DelegatedServiceConnectionGrant                                                  |
| Manager-SubmitContract-7       | Core       | Submit a Contract with a PeerRegistrationGrant combined with any another grant                            |
| Manager-SubmitContract-8       | Core       | Submit a Contract with multiple PeerRegistrationGrants                                                    |
| Manager-SubmitContract-9       | Core       | Submit a Contract with a ServicePublicationGrant combined with any another grant                          |
| Manager-SubmitContract-10      | Core       | Submit a Contract with a Group ID that does not match with the Group ID of the receiving Manager          |
| Manager-AcceptContract-1       | Core       | Place accept signature on a Contract                                                                      |
| Manager-AcceptContract-2       | Core       | Place accept signature on a Contract without being a Peer on the Contract                                 |
| Manager-AcceptContract-3       | Core       | Place accept signature which is not a valid JWS                                                           | 
| Manager-AcceptContract-4       | Core       | Place an accept signature of which the content hash does not match the contract content you are accepting |
| Manager-AcceptContract-5       | Core       | Place accept signature on a Contract with a signature type that is not accept                             |
| Manager-AcceptContract-6       | Core       | The hash in the request URL does not match with the contract hash of the contract in the request body     |
| Manager-RejectContract-1       | Core       | Place reject signature on a Contract                                                                      |
| Manager-RejectContract-2       | Core       | Place reject signature on a Contract without being a Peer on the Contract                                 |
| Manager-RejectContract-3       | Core       | Place reject signature which is not a valid JWS                                                           | 
| Manager-RejectContract-4       | Core       | Place a reject signature of which the content hash does not match the contract content you are rejecting  |
| Manager-RejectContract-5       | Core       | Place reject signature on a Contract with a signature type that is not reject                             |
| Manager-RejectContract-6       | Core       | The hash in the request URL does not match with the contract hash of the contract in the request body     |
| Manager-RevokeContract-1       | Core       | Place revoke signature on a Contract                                                                      |
| Manager-RevokeContract-2       | Core       | Place revoke signature on a Contract without being a Peer on the Contract                                 |
| Manager-RevokeContract-3       | Core       | Place revoke signature which is not a valid JWS                                                           | 
| Manager-RevokeContract-4       | Core       | Place a revoke signature of which the content hash does not match the contract content you are revoking   |
| Manager-RevokeContract-5       | Core       | Place revoke signature on a Contract with a signature type that is not revoke                             |
| Manager-RevokeContract-6       | Core       | The hash in the request URL does not match with the contract hash of the contract in the request body     |
| Manager-Contracts-1            | Core       | List Contracts                                                                                            |
| Manager-Contracts-2            | Core       | Do not list Contracts which do not contain the Peer                                                       |
| Manager-GetToken-1             | Core       | Request access token with a valid Contract                                                                |
| Manager-GetToken-2             | Core       | Request access token without a valid Contract                                                             |
| Manager-GetToken-3             | Core       | Request access token when the Contract has been revoked                                                   |
| Manager-GetToken-4             | Core       | Request access token with a Grant Hash that is in a invalid format                               |
| Manager-GetToken-5             | Core       | Request access token with an grant type that is not client_credentials                           |
| Manager-GetToken-6             | Delegation | Request access token with a valid Contract containing a DelegatedServiceConnectionGrant                   |
| Manager-GetToken-7             | Delegation | Request access token for a Service offered on behalf of a another Peer                                    |
| Manager-PeerInfo-1             | Core       | Get Peer information                                                                                      |
| Manager-Peers-1                | Core       | List Peers with a valid Contract containing a PeerRegistrationGrant                                       |
| Manager-Peers-2                | Core       | List Peers with whom Contracts have been negotiated                                                       |
| Manager-Services-1             | Core       | List Services with a valid Contract containing a ServicePublicationGrant                                  |
| Manager-TransactionLogRecord-1 | Logging    | List Transaction Log records                                                                              |
| Manager-Port-1                 | Core       | Accept request on port 443 or 8443                                                                        |
| Manager-JSONWebKeySet-1        | Core       | List keys used to sign signatures and/or access token                                                     |

# Manager-SubmitContract-1

Scenario: Submit a Contract
When a Contract with a ServiceConnectionGrant is submitted by the Peer
Then the Contract should be accepted

# Manager-SubmitContract-2

Scenario: Submit a Contract without being a Peer on the Contract
When a Contract is submitted by the Peer which does not include the Peer
Then the Contract should be rejected

# Manager-SubmitContract-3

Scenario: Submit a Contract
When a Contract with a PeerPublicationGrant is submitted by the Peer
Then the Contract should be accepted

# Manager-SubmitContract-4

Scenario: Submit a Contract
When a Contract with a ServicePublicationGrant is submitted by the Peer
Then the Contract should be accepted

# Manager-SubmitContract-5

Scenario: Submit a Contract
When a Contract with a DelegatedServicePublicationGrant is submitted by the Peer
Then the Contract should be accepted

# Manager-SubmitContract-6

Scenario: Submit a Contract
When a Contract with a DelegatedServiceConnectionGrant is submitted by the Peer
Then the Contract should be accepted

# Manager-SubmitContract-7

Scenario: Submit a Contract with a PeerRegistrationGrant and any other Grant
When a Contract is submitted by the Peer
Then the Contract should be rejected

# Manager-SubmitContract-8
Scenario: Submit a Contract with multiple PeerRegistrationGrants
When a Contract is submitted by the Peer
Then the Contract should be rejected

# Manager-SubmitContract-9

Scenario: Submit a Contract with a ServicePublicationGrant and any other Grant
When a Contract is submitted by the Peer
Then the Contract should be rejected

# Manager-SubmitContract-10

Scenario: Submit a Contract with a Group ID that does not match with the Group ID of the receiving Manager
When a Contract is submitted by the Peer
Then the Contract should be rejected

# Manager-AcceptContract-1

Scenario: Place accept signature on a Contract
Given a Contract without an accept signature of the Peer exists
When the Peer submits a valid accept signature
Then the Contract should contain the accept signature

# Manager-AcceptContract-2

Scenario: Place accept signature on a Contract without being a Peer on the Contract
Given a Contract exists that does not include the Peer
When the Peer submits an accept signature
Then signature should be rejected

# Manager-AcceptContract-3

Scenario: Place accept signature which is not a valid JWS
Given a Contract without an accept signature of the Peer exists
When the Peer submits an accept signature that is not a valid JWS
Then signature should be rejected

# Manager-AcceptContract-4

Scenario: Place an accept signature of which the content hash does not match the contract content you are accepting
Given a Contract without an accept signature of the Peer exists
When the Peers submits a signature which contains a content hash that does not match the contract content you are accepting
Then the signature should be rejected

# Manager-AcceptContract-5

Scenario: Place accept signature on a Contract with a signature type that is not accept
Given a Contract without an accept signature of the Peer exists
When the Peers submits a signature with a signature that is not of the type accept
Then the signature should be rejected

# Manager-AcceptContract-6

Scenario: The hash in the request URL does not match with the contract hash of the contract in the request body   
When the Peer submits an accept signature using a hash in the request URL that does not match the contract in the request body
Then the signature should be rejected

# Manager-RejectContract-1

Scenario: Place reject signature on a Contract
Given a Contract without a reject signature of the Peer exists
When the Peer submits a valid reject signature
Then the Contract should contain the reject signature

# Manager-RejectContract-2

Scenario: Place reject signature on a Contract without being a Peer on the Contract   
Given a Contract exists that does not include the Peer
When the Peer submits a reject signature
Then signature should be rejected

# Manager-RejectContract-3

Scenario: Place reject signature which is not a valid JWS
Given a Contract without an reject signature of the Peer exists
When the Peer submits an reject signature that is not a valid JWS
Then signature should be rejected

# Manager-RejectContract-4

Scenario: Place an reject signature of which the content hash does not match the contract content you are rejecting
Given a Contract without an reject signature of the Peer exists
When the Peers submits a signature which contains a content hash that does not match the contract content you are rejecting
Then the signature should be rejected

# Manager-RejectContract-5

Scenario: Place reject signature on a Contract with a signature type that is not reject
Given a Contract without an reject signature of the Peer exists
When the Peers submits a signature with a signature that is not of the type reject
Then the signature should be rejected

# Manager-RejectContract-6

Scenario: The hash in the request URL does not match with the contract hash of the contract in the request body   
When the Peer submits a reject signature using a hash in the request URL that does not match the contract in the request body
Then the signature should be rejected

# Manager-RevokeContract-1

Scenario: Place revoke signature on a Contract
Given a Contract without a revoke signature of the Peer exists
When the Peer submits a valid revoke signature
Then the Contract should contain the revoke signature

# Manager-RevokeContract-2

Scenario: Place revoke signature on a Contract without being a Peer on the Contract
Given a Contract exists that does not include the Peer
When the Peer submits a revoke signature
Then signature should be rejected

# Manager-RevokeContract-3

Scenario: Place revoke signature which is not a valid JWS
Given a Contract without an revoke signature of the Peer exists
When the Peer submits an revoke signature that is not a valid JWS
Then signature should be rejected

# Manager-RevokeContract-4

Scenario: Place an revoke signature of which the content hash does not match the contract content you are revokeing
Given a Contract without an revoke signature of the Peer exists
When the Peers submits a signature which contains a content hash that does not match the contract content you are revokeing
Then the signature should be rejected

# Manager-RevokeContract-5

Scenario: Place revoke signature on a Contract with a signature type that is not revoke
Given a Contract without an revoke signature of the Peer exists
When the Peers submits a signature with a signature that is not of the type revoke
Then the signature should be rejected

# Manager-RevokeContract-6

Scenario: The hash in the request URL does not match with the contract hash of the contract in the request body   
When the Peer submits an accept signature using a hash in the request URL that does not match the contract in the request body
Then the signature should be rejected

# Manager-Contracts-1

Scenario: List Contracts          
Given a valid Contract exists with a ServiceConnectionGrant containing the Peer
When the Contracts endpoint is called by the Peer
Then the Contract with the ServiceConnectionGrant is returned

# Manager-Contracts-2

Scenario: Do not list Contracts which do not contain the Peer  
Given a valid Contract exists with a ServiceConnectionGrant not containing the Peer
When the Contract endpoint is called by the Peer
Then the Contract with the ServiceConnection should not be returned

# Manager-GetToken-1

Scenario: Request access token with a valid Contract
Given a valid Contract exists with a ServiceConnectionGrant containing the Peer
When the Peer requests an access token
Then the access token should be returned

# Manager-GetToken-2

Scenario: Request access token without a valid Contract    
Given no valid Contract exists with a ServiceConnectionGrant containing the Peer
When the Peer requests an access token
Then the access token request should be rejected

# Manager-GetToken-3

Scenario: Request access token when the Contract has been revoked
Given a Contract with a ServiceConnectionGrant containing the Peer exists 
And the Contract has accept signatures of all Peers
And the Contract has a revoke signature of a Peer
When the Peer requests an access token
Then an access token containing the Delegator should be returned

# Manager-GetToken-4

Scenario: Request access token with a Grant Hash that is in an invalid format       
When the Peer requests an access token with a Grant Hash that is in an invalid format
Then an access token request should be rejected

# Manager-GetToken-5

Scenario: Request access token with a grant type that is not client_credentials
When the Peer requests an access token with a grant type that is not client_credentials
Then an access token request should be rejected

# Manager-GetToken-6

Scenario: Request access token with a valid Contract containing a DelegatedServiceConnectionGrant    
Given a valid Contract exists with a DelegatedServiceConnectionGrant containing the Peer
When the Peer requests an access token
Then an access token containing the Delegator should be returned

# Manager-GetToken-7

Scenario: Request access token for a Service offered on behalf of another Peer
Given a valid Contract exists with a ServiceConnectionGrant containing the Peer
And the Service is registered to the Directory with a Contract containing a DelegatedServicePublicationGrant  
When the Peer requests an access token
Then an access token containing the Delegator should be returned

# Manager-PeerInfo-1

Scenario: Get Peer information  
When the PeerInfo endpoint is called
Then the information about the Peer hosting the Manager should be returned

# Manager-Peers-1

Scenario: List Peers with a valid Contract containing a PeerRegistrationGrant
Given a valid Contract exists containing a PeerRegistrationGrant
When the Peers endpoint is called
Then the Peer described in the PeerRegistrationGrant should be returned

# Manager-Peers-2

Scenario: List Peers with whom Contracts have been negotiated          
Given a Peer has negotiated Contracts with Peers
When the Peers endpoint is called
Then the Peers with whom Contracts where negotiated should be returned

# Manager-Services-1

Scenario: List Services with a valid Contract containing a ServicePublicationGrant
Given a valid Contract exists containing a ServicePublicationGrant
When the Services endpoint is called
Then the Service described in the ServicePublicationGrant should be returned

# Manager-TransactionLogRecords-1

Scenario: List TransactionLog records
Given TransactionLog records containing the Peer exits  
When the logs endpoint is called
Then TransactionLog records containing the Peer should be returned

# Manager-Port-1

Scenario: Accept request on port 443 or 8443
When a request is sent to either port 443 or 8443
Then the Manager should respond

# Manager-JSONWebKeySet-1

Scenario: List keys used to sign signatures and/or access token
When the JSON WebKey Set endpoint is called 
Then the keys used by the Peer should be returned