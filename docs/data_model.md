# Data Model

## Fact Table
### FactClaim
- ClaimID
- CustomerID
- PolicyNumber
- HandlerID
- ClaimCreateDate
- ClaimCloseDate
- ClaimAmount
- IncidentType
- IncidentSeverity
- VehicleCount
- IsOpen
- ClaimDurationDays

## Dimension Tables
### DimCustomer
- CustomerID
- Age
- MaritalStatus
- CustomerSegment (Platinum / Standard)
- State

### DimPolicy
- PolicyNumber
- PolicyType
- CoverageType

### DimHandler
- HandlerID
- ReportingManager
- ExperienceLevel

### DimDate
- Date
- Year
- Month
- Quarter
