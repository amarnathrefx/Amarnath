# Prompt : [Busineess] Give me mark up to create ERD for https://mermaid.live/
## lease in Scenario in the Books of Lessee
```mermaid
erDiagram
    LEASE_CONTRACT {
        int LeaseContractID PK
        int LesseeID FK
        int LessorID FK
        date ContractStartDate
        date ContractEndDate
        int LeaseTerm
        string LeaseAssetDescription
        decimal DiscountRate
        decimal InitialROUValue
        decimal InitialLeaseLiability
    }

    ROU_ASSET {
        int ROUAssetID PK
        int LeaseContractID FK
        decimal OpeningBalance
        decimal Additions
        decimal DepreciationAccumulated
        decimal ClosingBalance
    }

    LEASE_LIABILITY {
        int LeaseLiabilityID PK
        int LeaseContractID FK
        decimal OpeningBalance
        decimal InterestAccrued
        decimal PaymentsMade
        decimal ClosingBalance
    }

    LEASE_PAYMENT {
        int LeasePaymentID PK
        int LeaseContractID FK
        date PaymentDate
        decimal PaymentAmount
        decimal PrincipalComponent
        decimal InterestComponent
    }

    DEPRECIATION {
        int DepreciationID PK
        int ROUAssetID FK
        string Period
        decimal DepreciationAmount
    }

    INTEREST_EXPENSE {
        int InterestID PK
        int LeaseLiabilityID FK
        string Period
        decimal InterestAmount
    }

    %% Relationships
    LEASE_CONTRACT ||--o{ ROU_ASSET : has
    LEASE_CONTRACT ||--o{ LEASE_LIABILITY : has
    LEASE_CONTRACT ||--o{ LEASE_PAYMENT : has
    ROU_ASSET ||--o{ DEPRECIATION : has
    LEASE_LIABILITY ||--o{ INTEREST_EXPENSE : has
```
## In the Books of Lessee with IND AS116 Scenario 02
``` mermaid
erDiagram
    LEASE_CONTRACT {
        int LeaseContractID PK
        int LesseeID FK
        int LessorID FK
        date ContractStartDate
        date ContractEndDate
        int LeaseTerm
        decimal DiscountRate
        decimal FairValueOfUnderlyingAsset
        decimal LeasePaymentAmount
        string PaymentFrequency
        decimal InitialDirectCosts
        decimal RestorationCosts
        decimal ResidualValueGuarantee
    }

    ROU_ASSET {
        int ROUAssetID PK
        int LeaseContractID FK
        decimal InitialMeasurement
        decimal AccumulatedDepreciation
        decimal NetBookValue
        date DepreciationStartDate
        date DepreciationEndDate
    }

    LEASE_LIABILITY {
        int LeaseLiabilityID PK
        int LeaseContractID FK
        decimal InitialLiability
        decimal RemainingLiability
        decimal InterestExpenseAccrued
    }

    LEASE_PAYMENT {
        int LeasePaymentID PK
        int LeaseContractID FK
        date PaymentDate
        decimal TotalPaymentAmount
        decimal InterestComponent
        decimal PrincipalComponent
    }

    DEPRECIATION {
        int DepreciationID PK
        int ROUAssetID FK
        date PeriodStart
        date PeriodEnd
        decimal DepreciationAmount
    }

    INTEREST_EXPENSE {
        int InterestExpenseID PK
        int LeaseLiabilityID FK
        date PeriodStart
        date PeriodEnd
        decimal InterestAmount
    }

    %% Relationships
    LEASE_CONTRACT ||--o{ ROU_ASSET : "gives rise to"
    LEASE_CONTRACT ||--o{ LEASE_LIABILITY : "gives rise to"
    LEASE_CONTRACT ||--o{ LEASE_PAYMENT : "requires"
    ROU_ASSET ||--o{ DEPRECIATION : "is depreciated by"
    LEASE_LIABILITY ||--o{ INTEREST_EXPENSE : "accrues"

```
