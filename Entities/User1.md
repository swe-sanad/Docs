@startuml
skinparam classAttributeIconSize 0

skinparam linetype ortho

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


class ContactInfo {
  +contactId: UUID
  +address: String
  +city: String
  +zip: String
  +state: String
  +country: String
  +phone: String
  +cell: String
  +email: String
  +vatId: String
  +nationalId: String  ' CNIC / ID
}

class AdminUser {
  +adminId: UUID
  +username: String
  +role: String
}

class UserGroup {
  +groupId: UUID
  +name: String
}

'========================
' Documents / KYC
'========================
class IdentityDocument {
  +documentId: UUID
  +type: String  ' CNIC/ID card
  +pageNumber: int
  +fileName: String
  +uploadedAt: DateTime
}

User "1" -- "0..*" IdentityDocument : documents >

User "1" -- "1" Account : owns >
User "0..*" -- "1" AdminUser : registeredBy >
Account "0..*" -- "1" AdminUser : owner >
Account "0..*" -- "1" UserGroup : memberOf >
User "1" o-- "0..1" ContactInfo : has >


@enduml