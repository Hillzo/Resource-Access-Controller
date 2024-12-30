# Resource Allocation Smart Contract

## Overview
This smart contract implements a comprehensive resource allocation system on the Stacks blockchain. It enables the management and distribution of resources with features including user authorization levels, resource type management, allocation requests, and emergency controls.

## Key Features
- Resource type registration and management
- Multi-tier user authorization system
- Request-based resource allocation
- Price history tracking
- Resource transfer capabilities
- Emergency controls and maintenance mode
- Blacklisting system for restricted accounts

## Authorization Levels
The contract supports five authorization levels:
1. `ADMIN` (Level 5) - Full administrative access
2. `PREMIUM` (Level 4) - Premium user access
3. `BUSINESS` (Level 3) - Business user access
4. `VERIFIED` (Level 2) - Verified user access
5. `USER` (Level 1) - Basic user access

## Core Functions

### System Management
1. `initialize-resource-system`
   - Initializes the contract
   - Can only be called once by the administrator

2. `update-system-parameters`
   - Updates global system parameters
   - Parameters: new allocation limit, new emergency admin address

### Resource Management
1. `register-resource-type`
   - Registers a new resource type
   - Parameters:
     - resource-type-identifier (uint)
     - resource-name (string-ascii 64)
     - initial-supply (uint)
     - unit-price (uint)
     - min-allocation (uint)
     - max-allocation (uint)
     - required-priority-level (uint)

2. `update-resource-price`
   - Updates the price of an existing resource
   - Maintains price history

### Account Management
1. `update-account-role`
   - Updates an account's authorization level
   - Only callable by administrator

2. `restrict-account`
   - Adds an account to the restricted list
   - Prevents access to resource operations

3. `remove-account-restriction`
   - Removes an account from the restricted list
   - Restores access to resource operations

### Resource Allocation
1. `submit-allocation-request`
   - Submits a new resource allocation request
   - Parameters:
     - resource-type-identifier
     - requested-quantity
     - allocation-purpose

2. `transfer-resources`
   - Transfers resources between accounts
   - Checks for sufficient balance and authorization

### Emergency Controls
1. `enable-maintenance-mode`
   - Enables system maintenance mode
   - Freezes all resource operations

2. `disable-maintenance-mode`
   - Disables maintenance mode
   - Resumes normal operations

3. `freeze-resource`
   - Freezes specific resource type
   - Prevents operations on that resource

4. `unfreeze-resource`
   - Unfreezes specific resource type
   - Resumes operations on that resource

## Error Codes
- `u100`: Unauthorized access
- `u101`: Invalid resource quantity
- `u102`: Insufficient resource balance
- `u103`: Resource type not found
- `u104`: Contract already initialized
- `u105`: Invalid recipient
- `u106`: Resource allocation exceeded
- `u107`: Insufficient priority
- `u108`: Resource frozen
- `u109`: Request timeout
- `u110`: Invalid parameters

## System Requirements
- Stacks blockchain compatibility
- Clarity smart contract support
- Standard principal address format support

## Security Considerations
1. **Access Control**
   - Multi-level authorization system
   - Administrator-only functions
   - Resource-specific access requirements

2. **Resource Protection**
   - Balance checks
   - Transfer limits
   - Frozen resource protection

3. **System Safety**
   - Emergency controls
   - Maintenance mode
   - Resource freezing capabilities

## Best Practices for Implementation
1. Always verify account authorization before operations
2. Monitor resource allocation limits
3. Maintain price history for auditing
4. Use maintenance mode for system updates
5. Regular monitoring of allocation requests
6. Implement proper error handling

## Example Usage

```clarity
;; Initialize the system
(contract-call? .resource-allocation initialize-resource-system)

;; Register a new resource type
(contract-call? .resource-allocation register-resource-type 
    u1                  ;; resource-type-identifier
    "Computing Power"   ;; resource-name
    u1000000           ;; initial-supply
    u100               ;; unit-price
    u10                ;; min-allocation
    u1000              ;; max-allocation
    u2)                ;; required-priority-level

;; Submit allocation request
(contract-call? .resource-allocation submit-allocation-request 
    u1                           ;; resource-type-identifier
    u100                        ;; requested-quantity
    "Production environment")    ;; allocation-purpose
```

## Maintenance and Updates
- Regular monitoring of system status
- Periodic review of resource allocations
- Update price parameters as needed
- Monitor and adjust allocation limits
- Regular security audits