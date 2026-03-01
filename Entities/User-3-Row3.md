@startuml
skinparam classAttributeIconSize 0

skinparam linetype ortho

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


class AuthLog {
  +authLogId: UUID
  +timestamp: DateTime
  +result: String
  +nasIp: String
  +callerId: String
}


class Subscription {
  +subscriptionId: UUID
  +startDate: Date
  +endDate: Date
  +autoRenew: bool
  +status: String
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


class NAS {
  +nasId: UUID
  +name: String
  +ip: String
}

class IPAssignment {
  +assignmentId: UUID
  +deviceRole: DeviceRole  ' CPE/CM
  +mode: IPMode
  +staticIp: String
}

class CMTS {
  +cmtsId: UUID
  +name: String
}

class AccessPoint {
  +apId: UUID
  +name: String
}

class QuotaPolicy {
  +quotaId: UUID
  +dailyDownBytes: long
  +dailyUpBytes: long
  +dailyTotalBytes: long
  +dailyOnlineSeconds: long
}

class PlanChange {
  +changeId: UUID
  +effectiveDate: DateTime
  +type: String  ' immediate/scheduled
  +requestedBy: String
}

class ServicePlan {
  +planId: UUID
  +name: String
  +downLimitBytes: long
  +upLimitBytes: long
  +totalLimitBytes: long
  +isAutoRenewEligible: bool
}


User "1" -- "1" Account : owns >

Account "1" -- "0..*" Invoice : invoices >
Account "1" -- "0..*" Payment : payments >
Account "1" -- "0..*" Deposit : deposits >
Account "1" o-- "0..*" RadiusAttribute : customAttrs >
Account "1" o-- "1" Subscription : subscribes >
Account "1" -- "0..*" TrafficUsage : usageRecords >
Account "1" o-- "0..1" NetworkProfile : network >
Account "1" -- "0..*" Session : sessions >

Account "1" -- "0..*" Invoice : invoices >
Account "1" -- "0..*" Payment : payments >
Account "1" -- "0..*" Deposit : deposits >

NetworkProfile "0..*" -- "0..1" NAS : viaNAS >

NetworkProfile "0..*" -- "0..1" AccessPoint : viaAP >
NetworkProfile "0..*" -- "0..1" CMTS : viaCMTS >
NetworkProfile "1" o-- "0..*" IPAssignment : ipAssignments >
IPAssignment "0..*" -- "0..1" IPPool : pool >
@enduml
