# Experiment 1: Decentralized Certificate Verification 
## Aim: 
To develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery 
and ensuring authenticity. 
## Algorithm: 
1. Deploy a smart contract where universities can issue certificates. 
 
2. Store a hash of certificate data on-chain. 
 
3. Provide a verification function that checks certificate authenticity. 
 
4. Users can verify the certificate by comparing the stored hash. 
 
## Code: 
```
// SPDX-License-Identifier: MIT 
pragma solidity ^0.8.20; 
 
contract CertificateVerification { 
    address public university; 
    mapping(bytes32 => bool) public certificates; // Store hashed certificates 
 
    event CertificateIssued(bytes32 indexed certHash); 
 
    constructor() { 
        university = msg.sender; // University deploys the contract 
    } 
 
    function issueCertificate(string memory studentName, string memory degree, 
uint256 year) public { 
        require(msg.sender == university, "Only university can issue 
certificates"); 
        bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, 
year)); 
        certificates[certHash] = true; 
        emit CertificateIssued(certHash); 
    } 
 
    function verifyCertificate(string memory studentName, string memory degree, 
uint256 year) public view returns (bool) { 
        bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, 
year)); 
        return certificates[certHash]; 
    } 
}
```
## Output:
### True
<img width="1435" height="992" alt="image" src="https://github.com/user-attachments/assets/1a57f7e1-930c-41fa-aab1-59987bbbc849" />

### False
<img width="1435" height="987" alt="image" src="https://github.com/user-attachments/assets/17dd2d91-f655-4686-9036-6885e9749d72" />

## Result:
Thus, the program to develop decentralized certificate verification is successfully executed. 
