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


class AdminUser {
  +adminId: UUID
  +username: String
  +role: String
}

class UserGroup {
  +groupId: UUID
  +name: String
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

User "1" -- "1" Account : owns >
User "0..*" -- "1" AdminUser : registeredBy >
Account "0..*" -- "1" AdminUser : owner >
Account "0..*" -- "1" UserGroup : memberOf >
User "1" o-- "0..1" ContactInfo : has >

'========================
' Authentication / RADIUS
'========================
class Credential {
  +credentialId: UUID
  +passwordHash: String
  +passwordType: PasswordType
  +simultaneousUse: int
  +pinFailedCount: int
  +verificationFailedCount: int
}

class RadiusAttribute {
  +attrId: UUID
  +name: String
  +operator: String
  +value: String
  +scope: String  ' check/reply/vendor/custom
}

class Verification {
  +verificationId: UUID
  +verificationCode: String
  +status: VerificationStatus
  +smsSentCount: int
}


Account "1" o-- "0..1" Credential : auth >
Account "1" o-- "0..*" RadiusAttribute : customAttrs >
Account "1" o-- "0..1" Verification : verification >

class AuthLog {
  +authLogId: UUID
  +timestamp: DateTime
  +result: String
  +nasIp: String
  +callerId: String
}

Account "1" -- "0..*" AuthLog : authenticationLog >

'========================
' Service & Subscription
'========================
class ServicePlan {
  +planId: UUID
  +name: String
  +downLimitBytes: long
  +upLimitBytes: long
  +totalLimitBytes: long
  +isAutoRenewEligible: bool
}

class Subscription {
  +subscriptionId: UUID
  +startDate: Date
  +endDate: Date
  +autoRenew: bool
  +status: String
}

class PlanChange {
  +changeId: UUID
  +effectiveDate: DateTime
  +type: String  ' immediate/scheduled
  +requestedBy: String
}

Account "1" o-- "1" Subscription : subscribes >
Subscription "1" -- "1" ServicePlan : plan >
Subscription "1" -- "0..*" PlanChange : changeHistory >
PlanChange "0..*" -- "0..1" ServicePlan : newPlan >

'========================
' Quota / Usage / Traffic
'========================
class QuotaPolicy {
  +quotaId: UUID
  +dailyDownBytes: long
  +dailyUpBytes: long
  +dailyTotalBytes: long
  +dailyOnlineSeconds: long
}

class TrafficUsage {
  +usageId: UUID
  +periodStart: DateTime
  +periodEnd: DateTime
  +downloadBytes: long
  +uploadBytes: long
  +totalBytes: long
  +onlineSeconds: long
}

Subscription "0..1" o-- "0..1" QuotaPolicy : dailyQuota >
Account "1" -- "0..*" TrafficUsage : usageRecords >

'========================
' Network Provisioning
'========================
class NetworkProfile {
  +networkProfileId: UUID
  +macCpe: String
  +macCm: String
  +allowThisMacOnly: bool
  +connectionStatus: String
}

class IPAssignment {
  +assignmentId: UUID
  +deviceRole: DeviceRole  ' CPE/CM
  +mode: IPMode
  +staticIp: String
}


class IPPool {
  +poolId: UUID
  +name: String
  +cidr: String
}

class NAS {
  +nasId: UUID
  +name: String
  +ip: String
}

class CMTS {
  +cmtsId: UUID
  +name: String
}

class AccessPoint {
  +apId: UUID
  +name: String
}

Account "1" o-- "0..1" NetworkProfile : network >
NetworkProfile "1" o-- "0..*" IPAssignment : ipAssignments >
IPAssignment "0..*" -- "0..1" IPPool : pool >
NetworkProfile "0..*" -- "0..1" NAS : viaNAS >
NetworkProfile "0..*" -- "0..1" CMTS : viaCMTS >
NetworkProfile "0..*" -- "0..1" AccessPoint : viaAP >

class Session {
  +sessionId: UUID
  +startTime: DateTime
  +endTime: DateTime
  +terminateCause: String
  +cpeIp: String
  +cpeMac: String
  +callerId: String
  +nasId: String
}

Account "1" -- "0..*" Session : sessions >

' Optional: RF/WiFi/DOCSIS telemetry implied by "details" panel
class DeviceTelemetry {
  +telemetryId: UUID
  +timestamp: DateTime
  +usPower: Decimal
  +usSnr: Decimal
  +usCcq: Decimal
  +dsSnr: Decimal
  +cmUptimeSeconds: long
  +cmReceivePower: Decimal
  +cmTransmitPower: Decimal
}

Session "0..*" o-- "0..1" DeviceTelemetry : telemetry >

'========================
' Billing / Finance
'========================
class Invoice {
  +invoiceId: UUID
  +issueDate: Date
  +dueDate: Date
  +amount: Decimal
  +status: String
}

class Payment {
  +paymentId: UUID
  +timestamp: DateTime
  +amount: Decimal
  +method: String
  +reference: String
}

class Deposit {
  +depositId: UUID
  +timestamp: DateTime
  +amount: Decimal
  +reference: String
}

Account "1" -- "0..*" Invoice : invoices >
Account "1" -- "0..*" Payment : payments >
Account "1" -- "0..*" Deposit : deposits >

'========================
' Alerts / Notifications
'========================
class AlertPreference {
  +alertPrefId: UUID
  +invoiceAlertEnabled: bool
  +smsAlertEnabled: bool
}

class AlertEvent {
  +alertEventId: UUID
  +type: String
  +sentAt: DateTime
  +channel: String
  +status: String
}

Account "1" o-- "0..1" AlertPreference : alertPrefs >
Account "1" -- "0..*" AlertEvent : alertsSent >

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

@enduml