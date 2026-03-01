@startuml
skinparam classAttributeIconSize 0

skinparam linetype ortho

enum AccountType {
  regular
  prepaid
  postpaid
}

enum AccountStatus {
  active
  suspended
  expired
  disabled
}


enum PasswordType {
  blank
  userDefined
  macAddress
}


enum VerificationStatus {
  notRequired
  pending
  verified
  failed
}


enum DeviceRole {
  CPE
  CM
}

enum IPMode {
  nasPoolOrDhcp
  ipPool
  staticIp
}




@enduml