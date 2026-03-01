@startuml
skinparam classAttributeIconSize 0

skinparam linetype ortho



'========================
' Core Identity / Account
'========================

class User {
  +userId: UUID
  +username: String
  +firstName: String
  +lastName: String
  +companyName: String
  +language: String
  +createdAt: DateTime
}

class Account {
  +accountId: UUID
  +accountType: AccountType
  +status: AccountStatus
  +registrationDate: Date
  +expiryDate: Date
  +balance: Decimal
  +currency: String
  +contractId: String
  +contractValidTill: Date
  +geoLat: Decimal
  +geoLong: Decimal
}



User "1" -- "1" Account : owns >
Account "0..*" -- "1" AdminUser : owner >
Account "0..*" -- "1" UserGroup : memberOf >

Account "1" o-- "0..1" Credential : auth >
Account "1" o-- "0..*" RadiusAttribute : customAttrs >
Account "1" o-- "0..1" Verification : verification >
Account "1" -- "0..*" AuthLog : authenticationLog >
Account "1" o-- "1" Subscription : subscribes >
Account "1" -- "0..*" TrafficUsage : usageRecords >
Account "1" o-- "0..1" NetworkProfile : network >
Account "1" -- "0..*" Session : sessions >

Account "1" -- "0..*" Invoice : invoices >
Account "1" -- "0..*" Payment : payments >
Account "1" -- "0..*" Deposit : deposits >
Account "1" o-- "0..1" AlertPreference : alertPrefs >
Account "1" -- "0..*" AlertEvent : alertsSent >


@enduml
