# OneBatch Guide

Integrate OneBatch to set up mapped payments to new or existing payee accounts by uploading a request file. You can use a single request file for all of the following operations:

* Register or update a payee's account.
* Register or update an external account, such as a bank or wire transfer account, for the payee to transfer their money.
* Register or update a physical or virtual prepaid card for the payee to transfer their money.
* Make a payment towards the payee account.

A merchant most often uses the following operations:

1.	Make an initial registration request and payment.
2.	Make subsequent payment requests.
3.	Update existing information.

After Hyperwallet processes the initial registration request, the payee receives an email that they can use to access the Pay Portal and complete additional fields as required.

## Supported file types

OneBatch supports XLS, XLSX, and XML file formats.

### Supported upload methods

Upload a OneBatch request file using SFTP or the Client Portal.

### Prerequisites

* You need to be authenticated to upload OneBatch requests.
* You need to be authenticated to upload OneBatch requests.
* You need to have the system privileges needed to use the Merchant Servicing Portal for relevant actions such as reviewing, approving, and processing requests.

Contact Hyperwallet Production Support at hwproductionsupport@paypal.com if you require assistance.

## Creating Request Files

Upload the payee’s initial registration information in an XLS, XLSX, or XML request file. You can also pass payment instructions in the request file. After processing the request, the system prompts payees for additional information during account activation, as specified in the program configuration.

### For XLS and XLSX

A OneBatch XLS or XLSX request file includes columns for the following types of information:

* Identifiers
* Profile
* Preferences
* External accounts
* Prepaid cards
* Payments

These types of information are described in the following section.

> **Note:** A typical OneBatch request file uses a small subset of possible column values. These columns correspond to real-world operations, such as creating a payee, adding an external account, or making a payment. This document's sample input formats and requirements follow a default program configuration. Your program configuration determines the information your request files need to include.

### Identifier columns

These columns identify the payee and their parent program. Be sure to specify the program and the payee.

| Column Heading | Description |
| ---: | :--- |
| **`progId.clientProgramId`**</br>string | The unique, client-assigned program identifier. You need to provide a `progId.clientProgramId` or `progId.programId` value. Max 75 characters. |
| **`progId.programId`**</br>number | The unique, Hyperwallet-assigned program number. You need to provide a `progId.clientProgramId` or `progId.programId value`. Maximum 20 digits. |
| **`custId.clientCustomerId`**</br>string | The unique, client-assigned identifier for the payee account. This ID can be any unique string. You need to provide a `custId.clientCustomerId`, `custId.walletNumber`, or `custId.inventoryControlNumber` value. Supports letters, numbers, and `+ , - . / _ ~`. Max 75 characters. |
| **`custId.walletNumber`**</br>number | The unique, Hyperwallet-assigned payee account number. You need to provide a `custId.clientCustomerId`, `custId.walletNumber`, or `custId.inventoryControlNumbervalue`. Maximum 28 digits. |
| **`custId.inventoryControlNumber`**</br>string | The unique, Hyperwallet-assigned inventory control number. You only need this information for instant issue card programs. You need to provide a `custId.clientCustomerId`, `custId.walletNumber`, or `custId.inventoryControlNumber` value. Max 45 characters. |

### Profile columns

These columns describe a payee's profile, including identification and address information. The column headings start with the prefix `profile.`.

> **Note:** You only need profile column values to create a user account for a payee or update a payee's profile.

| Column Heading | Description |
| ---: | :--- |
| **`profile.entityType`**</br>string | Identifies whether the payee is an individual or a business entity. Required if you want to create a user account. This parameter supports the following values:<ul><li>`INDIVIDUAL` : an individual external accountholder; default value.</li><li>`COMPANY`: a business.</li></ul> |
| **`profile.accountType`**</br>string | Identifies the type of business entity. Required if `profile.entityType = COMPANY`. This parameter supports the following values:<ul><li>`Individual`: an individual.</li><li>`Corporation`: a corporation.</li><li>`Partnership`: a partnership.</li><li>`CanadianRegisteredCharity`: a charity registered in Canada.</li></ul> |
| **`profile.firstName`**</br>string | The first name of the payee or business contact. Required if you want to create a user account and `profile.entityType = INDIVIDUAL`. This field supports letters, spaces, and `' , -`. Max 50 characters. |
| **`profile.middleName`**</br>string | The middle name of the payee or business contact. Use when `profile.firstName` and `profile.lastName` are provided. This field supports letters, spaces, and `' , -`. Max 50 characters. |
| **`profile.lastName`**</br>string | The last name of the payee or business contact. Required if you want to create a user account and `profile.entityType = INDIVIDUAL`. This field supports letters, spaces, and `' , -`. Max 100 characters. |
| **`profile.businessName`**</br>string | The business name. Required if you want to create a user account and `profile.entityType = COMPANY`. This field supports letters, numbers, spaces, and `! & ' ( ) + , - . / : ;`. Max 100 characters. |
| **`profile.businessRegistrationNumber`**</br>string | The business registration number. Use when `profile.entityType = COMPANY`. This field supports numbers, letters, spaces, and `( ) + - . /`. Max 100 characters. |
| **`profile.phoneNumber`**</br>string | The phone number of the payee or business contact. This field supports numbers, spaces, and `( ) . - +`. This field saves digits and strips out all other characters. Max 17 characters. |
| **`profile.mobileNumber`**</br>string | The cell phone number of the payee or business contact. This field supports numbers, spaces, and `( ) . - +`. This field saves digits and strips out all other characters. Max 17 characters. |
| **`profile.dateOfBirth`**</br>string | The date of birth of the payee or business contact. Format: `YYYY-MM-DD`. |
| **`profile.gender`**</br>string | The gender of the payee or business contact. This parameter supports the following values:<ul><li>`M`: male</li><li>`F`: female</li></ul> |
| **`profile.employerIdentificationNumber`**</br>string | The employer identifier that the payee uses for tax purposes. Applicable when `profile.entityType = COMPANY`. Max 10 characters. |
| **`profile.occupation`**</br>string | The field of work or job title of the payee or business contact. Max 50 characters. |
| **`profile.passportNumber`**</br>string | The passport number of the payee or business contact. Max 70 characters. |
| **`profile.passportPlaceOfBirth`**</br>string | The place of birth of the payee or business contact, as noted on their passport. Max 100 characters. |
| **`profile.passportIssuingCountry`**</br>string | The 2-letter ISO code of the country that has issued the passport to the payee or business contact. |
| **`profile.passportDateOfIssuance`**</br>string | The date the passport was issued to the payee or business contact. Format: `YYYY-MM-DD`. |
| **`profile.passportExpiryDate`**</br>string | The date the payee or business contact's passport expires. Format: `YYYY-MM-DD`. |
| **`profile.passportDepartmentalCode`**</br>string | The passport departmental code for the payee or business contact. Max 45 characters. |
| **`profile.governmentId`**</br>string | The government ID number of the payee or business contact. Examples include an SSN or SIN number). This field supports numbers, letters, spaces, and `( ) + - . / _`. Max 21 characters. |
| **`profile.governmentIdType`**</br>string | The government ID type that was used for the payee or business contact. Use when a `profile.governmentId` value was provided. Max 50 characters. |
| **`profile.driverLicenseNumber`**</br>string | The driver's license number of the payee or business contact. Max 70 characters. |
| **`profile.driverLicenseJurisdiction`**</br>string | The state, province, or region that issued the driver’s license to the payee or business contact. Max 200 characters. |
| **`profile.countryOfBirth`**</br>string | The 2-letter ISO code of the payee's or business contact's birth country. |
| **`profile.citizenshipCountry`**</br>string | The 2-letter ISO code of the payee's or business contact's country of nationality. |
| **`profile.businessRegistrationStateProv`**</br>string | The state, province, or region where the business is registered. Use when `profile.entityType = COMPANY`. This field supports letters, spaces, and `& ' ( ) -`. Max 50 characters. |
| **`profile.businessRegistrationCountry`**</br>string | The 2-letter ISO code of the country where the business is registered. Use when `profile.entityType = COMPANY`. |
| **`profile.businessContactRole`**</br>string | The formal position or job title of the business contact. Applicable when `profile.entityType = COMPANY`. This field supports the following values:<ul><li>`OWNER`</li><li>`DIRECTOR`</li><li>`OTHER`</li></ul> |
| **`profile.street`**</br>string | The payee's street address. This field supports letters, numbers, spaces, and `# ' ( ) , - . / : ; °`. Max 100 characters. |
| **`profile.addressLine2`**</br>string | The payee's address line 2. Applicable when a `profile.street` value is provided. This field supports letters, numbers, spaces, and `# ' ( ) , - . / : ; °`. Max 100 characters. |
| **`profile.addressLine3`**</br>string | The payee's address line 3. Applicable when a `profile.addressLine2` value is provided. This field supports letters, numbers, spaces, and `# ' ( ) , - . / : ; °`. Max 100 characters. |
| **`profile.city`**</br>string | The payee's city. This field supports letters, spaces, and `& ' ( ) -`. Max 50 characters. |
| **`profile.stateProv`**</br>string | The payee's state, province, or region. Use when the payee's `profile.country` has states, provinces or regions. This field supports letters, spaces, and `& ' ( ) -`. Max 50 characters. |
| **`profile.country`**</br>string | The payee's 2-letter ISO country code. |
| **`profile.postCode`**</br>string | The payee's ZIP code, postal code, or equivalent. Use when the payee's `profile.country` uses ZIP codes, postal codes or equivalent identifiers. This field supports numbers, letters, spaces, and `-`. Max 16 characters. |

## Preference columns

These columns describe a payee's Pay Portal account preferences. The column headings start with the prefix `prefs.`.

> **Note:** You only need preference column values to create a user account for a payee or update a payee's preferences.

| Column Heading | Description |
| ---: | :--- |
| **`prefs.emailAddress`**</br>string | The contact email address for the payee. Account notification emails are sent to this email address. Required if you want to create a user account. Max 200 characters; needs to be a valid email address. |
| **`prefs.timeZone`**</br>string | The preferred time zone for the payee's account. Defaults to Greenwich Mean Time (`GMT`) if left blank or if an incorrect time zone ID is supplied. |
| **`prefs.language`**</br>string | The preferred language for the payee's account. Defaults to English (`en`) if left blank or an incorrect language code is supplied. |

## External Account columns

These columns describe an external account associated with a payee. Examples include bank accounts with direct deposit, wire transfer accounts, and paper check accounts.

The column headings start with the prefix `ea.`.

When the payee and external accountholder are the same person, Hyperwallet uses the payee's profile values for the external accountholder's profile, starting with `ea.entityType`.

Set up your integration to:

* Explicitly require external accountholder profile values.
* Permit an external accountholder that isn't the payee.

If you or the payees have already provided the profile information, you can skip the profile information columns in the `ea.` section.

> **Note:** External account column values are only needed when you are registering or updating a payee's external account. The following table lists all available external account columns. The exact data requirements epend on the country-specific bank account with direct deposit, wire transfer, or paper check accounts.

| Column Heading | Description |
| ---: | :--- |
| **`ea.externalAccountType`**</br>string</br>required | The external account type. Fixed string. Supported values are determined by the country-specific direct-deposit bank account, wire transfer, or paper check account. Every program needs to have an external account type. |
| **`ea.currencyCode`**</br>string</br>required | The 3-letter code for the currency of the external account. Supported values are determined by the `ea.externalAccountType`. |
| **`ea.bankName`**</br>string | The bank name. Max 100 characters. |
| **`ea.bankCode`**</br>string | The bank code, Bank Identification Code (BIC), Society for Worldwide Interbank Financial Telecommunication (SWIFT) code, or equivalent. Max 15 characters. |
| **`ea.branchName`**</br>string | The branch name. Max 50 characters. |
| **`ea.branchCode`**</br>string | The branch code, branch transit number, routing number, or equivalent. Max 15 characters. |
| **`ea.accountNumber`**</br>string | The bank or wire transfer account number. Max 50 characters. |
| **`ea.accountRelationship`**</br>string | <p>The user's relationship with the bank accountholder. Optional. This parameter supports the following values:</p><p>For individual payees</br>`RELATIONSHIP_SELF`: the user owns the bank account.</p><p>For business payees</br>`RELATIONSHIP_OWN_COMPANY`: the bank account is owned by the user's business.</p> |
| **`ea.accountPurpose`**</br>string | The purpose of the bank account, such as savings or checking. Fixed string. The external account type determines the supported values. |
| **`ea.displayName`**</br>string | A user-friendly name for an account. This name shows up on the Pay Portal. Required if updating an external account, but otherwise optional. If you don't provide an `ea.displayName` when adding the external account, Hyperwallet automatically generates a value for the payee. Find this value using the Pay Portal. Max 100 characters. |
| **`ea.taxId`**</br>string | The external accountholder's tax identifier. Only use this parameter for Russian bank accountholders with `entityType = COMPANY`. Max 12 characters. |
| **`ea.taxRegistrationReasonCode`**</br>string | The external accountholder's tax registration reason code. Only use this parameter for Russian bank accountholders. Max 18 characters. |
| **`ea.agreementDate`**</br>string | The direct deposit agreement date for the bank account. This only applies to BACSbanks. |
| **`ea.securityQuestion`**</br>string | A security question to verify the external accountholder's identity. This only applies to MoneyGram accounts. Max 500 characters. |
| **`ea.securityAnswer`**</br>string | The response to an `ea.securityQuestion`. Max 500 characters. |
| **`ea.reference`**</br>string | A reference number. This only applies to MoneyGram accounts. Max 53 characters. |
| **`ea.instructions`**</br>string | Instructions for the external accountholder. This only applies to MoneyGram accounts. Max 500 characters. |
| **`ea.isDefaultCashoutAccount`**</br>boolean | When true, this account is the default auto-cashout account for the user. Default: `false`. |
| **`ea.additionalField1`**</br>string | Additional identifier 1. This only applies to WUBS wire transfer accounts. This only applies to MoneyGram accounts. |
| **`ea.additionalField2`**</br>string | Additional identifier 2. This only applies to WUBS wire transfer accounts. This only applies to MoneyGram accounts. |
| **`ea.bankAddress.street`**</br>string | The bank's street address. Max 2000 characters. |
| **`ea.bankAddress.addressLine2`**</br>string | Line 2 of the bank's address. Use this field if an `ea.bankAddress.street` value is provided. Max 100 characters. |
| **`ea.bankAddress.addressLine3`**</br>string | Line 3 of the bank's address. Use this field if an `ea.bankAddress.addressLine2` value is provided. Max 100 characters. |
| **`ea.bankAddress.city`**</br>string | The bank's city. Max 128 characters. |
| **`ea.bankAddress.stateProv`**</br>string | The bank's state, province, or region. Use this field if the payee's `ea.bankAddress.country` has states, provinces, or regions. Max 100 characters. |
| **`ea.bankAddress.country`**</br>string | The bank's 2-letter ISO country code. |
| **`ea.bankAddress.postCode`**</br>string | The bank's ZIP code, postal code, or equivalent. Use this field if the payee's ea.bankAddress.country uses ZIP codes, postal codes, or equivalent identifiers. Max 32 characters. |
| **`ea.intermediaryBankName`**</br>string | The intermediary bank name. This only applies to wire transfer accounts. Max 50 characters. |
| **`ea.intermediaryBankCode`**</br>string | The intermediary bank code, BIC/SWIFT code, or equivalent. This only applies to wire transfer accounts. Max 25 characters. |
| **`ea.intermediaryBranchCode`**</br>string | The intermediary branch code, branch transit number, routing number, or equivalent. This only applies to wire transfer accounts. Max 25 characters. |
| **`ea.intermediaryAccountNumber`**</br>string | The intermediary bank or wire transfer account number. This only applies to wire transfer accounts. Max 100 characters. |
| **`ea.intermediaryAddress.street`**</br>string | The intermediary bank's street address. Max 2000 characters. |
| **`ea.intermediaryAddress.addressLine2`**</br>string | Line 2 of the intermediary bank's address. Use this field if an `ea.intermediaryAddress.street` value is provided. Max 100 characters. |
| **`ea.intermediaryAddress.addressLine3`**</br>string | Line 3 of the intermediary bank's address. Use this field if an `ea.intermediaryAddress.addressLine2` value is provided. Max 100 characters. |
| **`ea.intermediaryAddress.city`**</br>string | The intermediary bank's city. Max 128 characters. |
| **`ea.intermediaryAddress.stateProv`**</br>string | The intermediary bank's state, province, or region. Use this field if the payee's `ea.intermediaryAddress.country` has states, provinces or regions. Max 100 characters. |
| **`ea.intermediaryAddress.country`**</br>string | The intermediary bank's 2-letter ISO country code. |
| **`ea.intermediaryAddress.postCode`**</br>string | The intermediary bank's ZIP code, postal code, or equivalent. Use this field if the payee's `ea.intermediaryAddress.country` uses ZIP codes, postal codes, or equivalent identifiers. Max 32 characters. |
| **`ea.entityType`**</br>string | Identifies whether the external accountholder is an individual or a business entity. Required if you want to create an external account. This parameter supports the following values:<ul><li>`INDIVIDUAL` : an individual external accountholder; default value</li><li>`COMPANY`: a business</li></ul> |
| **`ea.accountType`**</br>string | Identifies the type of business entity. Use this field if `ea.entityType = COMPANY`. This parameter supports the following values:<ul><li>`Individual`: an individual</li><li>`Corporation`: a corporation</li><li>`Partnership`: a partnership</li><li>`CanadianRegisteredCharity`: a charity registered in Canada</li></ul> |
| **`ea.firstName`**</br>string | The first name of the external accountholder or business contact. Required if you want to create an external account and `ea.entityType = INDIVIDUAL`. Max 50 characters. |
| **`ea.middleName`**</br>string | The middle name of the external accountholder or business contact. Use this field if `ea.firstName` and `ea.lastName` are provided. Max 50 characters. |
| **`ea.lastName`**</br>string | The last name of the external accountholder or business contact. Required if you want to create an external account and `ea.entityType = INDIVIDUAL`. Max 50 characters. |
| **`ea.businessName`**</br>string | The business name. Required if you want to create an external account and `ea.entityType = COMPANY`. Max 100 characters. |
| **`ea.businessRegistrationNumber`**</br>string | The business registration number. Use this field if `ea.entityType = COMPANY`. Max 100 characters. |
| **`ea.phoneNumber`**</br>string | The phone number of the external accountholder or business contact. This field saves digits and strips out all other characters. Max 35 characters. |
| **`ea.mobileNumber`**</br>string | The cell phone number of the external accountholder or business contact. This field saves digits and strips out all other characters. Max 35 characters. |
| **`ea.dateOfBirth`**</br>string | The date of birth of the external accountholder or business contact. Format: `YYYY-MM-DD`. |
| **`ea.gender`**</br>string | The gender of the external accountholder or business contact. This parameter supports the following values:<ul><li>`M`: male</li><li>`F`: female</li></ul> |
| **`ea.employerIdentificationNumber`**</br>string | The employer identifier that the external accountholder uses for tax purposes. Use this field if `ea.entityType = COMPANY`. Max 10 characters. |
| **`ea.occupation`**</br>string | The field of work or job title of the external accountholder or business contact. Max 50 characters. |
| **`ea.passportNumber`**</br>string | The passport number of the external accountholder or business contact. Max 70 characters. |
| **`ea.passportPlaceOfBirth`**</br>string | The place of birth of the external accountholder or business contact, as noted on their passport. Max 100 characters. |
| **`ea.passportIssuingCountry`**</br>string | The 2-letter ISO code of the country that has issued the passport to the external accountholder or business contact. |
| **`ea.passportDateOfIssuance`**</br>string | The date the passport was issued to the external accountholder or business contact. Format: `YYYY-MM-DD`. |
| **`ea.passportExpiryDate`**</br>string | The date the external accountholder’s or business contact's passport expires. Format: `YYYY-MM-DD`. |
| **`ea.passportDepartmentalCode`**</br>string | The passport departmental code for the external accountholder or business contact. Max 45 characters. |
| **`ea.governmentId`**</br>string | The external accountholder’s or business contact's government ID number, such as an SSN or SIN number. Max 70 characters. |
| **`ea.governmentIdType`**</br>string | The government ID type that was used for the external accountholder or business contact. Use this field if an `ea.governmentId` value was provided. Max 50 characters. |
| **`ea.driverLicenseNumber`**</br>string | The external accountholder’s or business contact's driver's license number. Max 70 characters. |
| **`ea.driverLicenseJurisdiction`**</br>string | The state, province, or region that issued the external accountholder’s or business contact's driver’s license. Max 200 characters. |
| **`ea.countryOfBirth`**</br>string | The 2-letter ISO code of the external accountholder's or business contact's birth country. |
| **`ea.citizenshipCountry`**</br>string | The 2-letter ISO code of the external accountholder's or business contact's country of nationality. |
| **`ea.businessRegistrationStateProv`**</br>string | The state, province, or region where the business is registered. Use this field if `ea.entityType = COMPANY`. Max 100 characters. |
| **`ea.businessRegistrationCountry`**</br>string | The 2-letter ISO code of the country where the business is registered. Use this field if `ea.entityType = COMPANY`. |
| **`ea.businessContactRole`**</br>string | The formal position or job title of the business contact. Use this field if `ea.entityType = COMPANY`. This parameter supports the following values:<ul><li>`OWNER`</li><li>`DIRECTOR`</li><li>`OTHER`</li></ul> |
| **`ea.street`**</br>string | The external accountholder's street address. Max 2000 characters. |
| **`ea.addressLine2`**</br>string | Line 2 of the external accountholder's address. Use this field if an `ea.street` value is provided. Max 100 characters. |
| **`ea.addressLine3`**</br>string | Line 3 of the external accountholder's address. Use this field if an `ea.addressLine2value` is provided. Max 100 characters. |
| **`ea.city`**</br>string | The external accountholder's city. Max 128 characters. |
| **`ea.stateProv`**</br>string | The external accountholder's state, province, or region. | Use this field if the external accountholder's `ea.country` has states, provinces, or regions. Max 100 characters. |
| **`ea.country`**</br>string | The external accountholder's 2-letter ISO country code. |
| **`ea.postCode`**</br>string | The external accountholder's ZIP code, postal code, or equivalent. Use this field if the external accountholder's `ea.country` uses ZIP codes, postal codes, or equivalent identifiers. Max 32 characters. |

## Prepaid Card columns

These columns describe a prepaid card. The column headings start with the prefix `ppc.`.

When the payee and external accountholder are the same person, Hyperwallet uses the payee's profile values for the cardholder's profile, starting with `ppc.entityType`.

> **Note:** Only provide prepaid card column values if you are requesting or updating a prepaid card for the payee.

| Column Heading | Description |
| ---: | :--- |
| **`ppc.packageName`**</br>string | The card package name. Required when requesting a prepaid card. The card package name can't be updated. Needs to be a valid card package configured for the program. |
| **`ppc.entityType`**</br>string | Identifies whether the cardholder is an individual or a business entity. Required if you want to create a user account. This parameter supports the following values:<ul><li>`INDIVIDUAL`: an individual payee; default value</li><li>`COMPANY`: a business</li></ul> |
| **`ppc.accountType`**</br>string | Identifies the type of business entity. Required when `ppc.entityType = COMPANY`. This parameter supports the following values:<ul><li>`Individual`: an individual payee</li><li>`Corporation`: a corporations</li><li>`Partnership`: a partnership</li><li>`CanadianRegisteredCharity`: a charity registered in Canada</li></ul> |
| **`ppc.firstName`**</br>string | The first name of the cardholder or business contact. Required if you want to create a prepaid card account and `ppc.entityType = INDIVIDUAL`. Max 50 characters. |
| **`ppc.middleName`**</br>string | The middle name of the cardholder or business contact. Use when `ppc.firstName` and `ppc.lastName` are provided. Max 50 characters. |
| **`ppc.lastName`**</br>string | The last name of the cardholder or business contact. Required if you want to create a prepaid card account and `ppc.entityType = INDIVIDUAL`. Max 50 characters. |
| **`ppc.businessName`**</br>string | The business name. Required if you want to create a prepaid card account and `ppc.entityType = COMPANY`. Max 100 characters. |
| **`ppc.businessRegistrationNumber`**</br>string | The business registration number. Use when `ppc.entityType = COMPANY`. Max 100 characters. |
| **`ppc.phoneNumber`**</br>string | The phone number of the cardholder or business contact. This field saves digits and strips out all other characters. Max 35 characters. |
| **`ppc.mobileNumber`**</br>string | The cell phone number of the cardholder or business contact. This field saves digits and strips out all other characters. Max 35 characters. |
| **`ppc.dateOfBirth`**</br>string | The date of birth of the cardholder or business contact. Format: `YYYY-MM-DD`. |
| **`ppc.gender`**</br>string | The gender of the cardholder or business contact. his parameter supports the following values:<ul><li>`M`: male</li><li>`F`: female</li></ul> |
| **`ppc.employerIdentificationNumber`**</br>string | The employer identifier that the cardholder uses for tax purposes. Use when `ppc.entityType = COMPANY`. Max 10 characters. |
| **`ppc.occupation`**</br>string | The field of work or job title of the cardholder or business contact. Max 50 characters. |
| **`ppc.passportNumber`**</br>string | The passport number of the cardholder or business contact. Max 70 characters. |
| **`ppc.passportPlaceOfBirth`**</br>string | The place of birth of the cardholder or business contact, as noted on their passport. Max 100 characters. |
| **`ppc.passportIssuingCountry`**</br>string | The 2-letter ISO code of the country that issued the passport to the cardholder or business contact passport. |
| **`ppc.passportDateOfIssuance`**</br>string | The date the passport was issued to the cardholder or business contact. Format: `YYYY-MM-DD`. |
| **`ppc.passportExpiryDate`**</br>string | The date the cardholder’s or business contact's passport expires. Format: `YYYY-MM-DD`. |
| **`ppc.passportDepartmentalCode`**</br>string | The passport departmental code for the cardholder or business contact. Max 45 characters. |
| **`ppc.governmentId`**</br>string | The government ID number of the cardholder or business contact, such as an SSN or SIN number. Max 70 characters. |
| **`ppc.governmentIdType`**</br>string | The government ID type that was used for the cardholder or business contact. Use when a `ppc.governmentId` value was provided. Max 50 characters. |
| **`ppc.driverLicenseNumber`**</br>string | The driver's license number of the cardholder or business contact. Max 70 characters. |
| **`ppc.driverLicenseJurisdiction`**</br>string | The state, province, or region that issued the driver’s license to the cardholder or business contact. Max 200 characters. |
| **`ppc.countryOfBirth`**</br>string | The 2-letter ISO code of the cardholder's or business contact's birth country. |
| **`ppc.citizenshipCountry`**</br>string | The 2-letter ISO code of the cardholder's or business contact's country of nationality. |
| **`ppc.businessRegistrationStateProv`**</br>string | The state, province, or region where the business is registered. Use when `ppc.entityType = COMPANY`. Max 100 characters. |
| **`ppc.businessRegistrationCountry`**</br>string | The 2-letter ISO code of the country where the business is registered. Use when `ppc.entityType = COMPANY`. |
| **`ppc.businessContactRole`**</br>string | The formal position or job title of the business contact. Use when `ppc.entityType = COMPANY`. This parameter supports the following values:<ul><li>`OWNER`</li><li>`DIRECTOR`</li><li>`OTHER`</li></ul> |
| **`ppc.street`**</br>string | The cardholder's street address. Max 2000 characters. |
| **`ppc.addressLine2`**</br>string | The cardholder's address line 2. Use when a `ppc.street` value is provided. Max 100 characters. |
| **`ppc.addressLine3`**</br>string | The cardholder's address line 3. Use when a `ppc.addressLine2` value is provided. Max 100 characters. |
| **`ppc.city`**</br>string | The cardholder's city. Max 128 characters. |
| **`ppc.stateProv`**</br>string | The cardholder's state, province, or region. Use when the cardholder's `ppc.country` has states, provinces or regions. Max 100 characters. |
| **`ppc.country`**</br>string | The cardholder's 2-letter ISO country code. |
| **`ppc.postCode`**</br>string | The cardholder's ZIP code, postal code or equivalent. Use when the cardholder's `ppc.country` uses ZIP codes, postal codes or equivalent identifiers. Max 32 characters. |

## Payment columns

These columns describe a payment made to the payee. The column headings start with the prefix `payment.`.

> **Note:** Only provide payment column values if you are making a payment. You can't update past payments.

| Column Heading | Description |
| ---: | :--- |
| **`payment.fundingClientProgramId`**</br>string | The custom ID of the program that is making the payment. Needs to match the program's external group ID in the Merchant Servicing Portal. Only applies if the program is configured to support this field. Provide either a `payment.fundingClientProgramId` value or a `payment.fundingProgramId value`. If left blank, the money comes from the payee's parent program. Max 75 characters. |
| **`payment.fundingProgramId`**</br>number | The Hyperwallet ID of the program that is making the payment. Maximum 28 digits. Only applies if the program is configured to support this field. Provide either a `payment.fundingClientProgramId` value or a `payment.fundingProgramId` value. If left blank, the money comes from the payee's parent program. |
| **`payment.valueDate`**</br>string | The date when the money releases. The payment is queued for processing at GMT 00:00:00 (12:00 AM) on the specified date. A blank value implies that the payment is be queued for processing immediately. |
| **`payment.expiryDate`**</br>string | The date when the payment funds expire. The expiration is processed at GMT 00:00:00 (12:00 AM) on the specified date. After this time, the money is no longer available. A blank value implies that there is no expiration date. |
| **`payment.amount`**</br>string</br>required | The payment amount. Needs to contain the appropriate number of decimal points for the currency in `payment.currencyCode`. Max 20 characters. |
| **`payment.currencyCode`**</br>string</br>required | The payment currency. Needs to be a supported 3-letter currency code that is configured for the program. |
| **`payment.clientReferenceNumber`**</br>string</br>required | The client-assigned reference number for the transaction. Max 50 characters. |
| **`payment.purposeOfPayment`**</br>string</br>required | The purpose of the payment. Needs to be a valid purpose code. |
| **`payment.description`**</br>string | A transaction description provided by the client. The payee can see this description. Max 200 characters. |
| **`payment.memo`**</br>string | An internal memo for the transaction. Not visible to the payee. Max 50 characters. |
| **`payment.securityQuestion`**</br>string | A security question to verify the payee's identity. Max 100 characters. |
| **`payment.securityAnswer`**</br>string | The response to `payment.securityQuestion`. Max 100 characters. |

### Uploading requests

Upload a batch request file using the Client Portal or SFTP.

#### Uploading using the Client Portal

![Upload Batch Jobs](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch_uploadjobs.png "The upload batch jobs screen has a button to choose a program for the batch job, a pulldown menu for batch type, a button named select file, a text entry field labelled file reference, and 2 radio buttons labelled process immediately and process at a schedule date and time. Process immediately is selected. After that is an entry field labelled process day and time, with a calendar icon, and a note showing that the calendar is in Greenwich Mean Time. After this is a button labelled upload file.")

1.	Select a **Batch Processing** in the left menu of the Client Portal.
2.	Select a **Upload Batch Jobs**.
3.	Select your program ID from the treeview, after the **Filter** field. You can also use the **Filter** field to filter your program ID.
4.	Select your intended batch type from the **Batch Type** dropdown.
5.	Select **Choose File** and browse to the request file you want to upload.
6.	Enter a **File Reference** value to uniquely identify the data set in the upload file. If you leave this blank, the filename is used.
7.	Select **Process Immediately** to queue the request file for processing immediately, or **Process At Scheduled Date/Time** to do request processing in the future. Select the calendar icon to choose the date and time.
8.	Select **Upload File**.

After you upload the file, the page shows a message indicating that the upload is successful, or an error message explaining why it wasn't successful.

> **Note:** The program ID selected in step 3 needs to match the one specified in your request data, or be superior to it in your program hierarchy.

![Batch, Successful Upload](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch_uploadsuccess.png "The upload batch jobs screen shows a message saying that the file was successfully loaded, and includes the name of the file. After this is a button to choose a program for the batch job, a pulldown menu for batch type, a button named select file, a text entry field labelled file reference, and 2 radio buttons labelled process immediately and process at a schedule date and time. Process immediately is selected. After that is an entry field labelled process day and time, with a calendar icon, and a note showing that the calendar is in Greenwich Mean Time. After this is a button labelled upload file. After this are buttons labelled view batch and batch list.")

#### Uploading using SFTP

To learn more about submitting OneBatch files, see [Uploading Requests](https://portal.hyperwallet.com/docs/batch/v2/uploading-requests).

### Managing batch jobs

After you upload a request file, manage the batch job from the following pages in the Client Portal:

#### Using the Batch Overview page

The **Batch Overview** page shows the current overview of a job. Use this page to complete actions on the batch job, such as approve or process.

![batch-overviewpage.png](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-overviewpage.png "The batch overview screen shows the name of the file, followed by a link labelled batch step. There is a table with 6 batch steps: file upload, file approval, file schedule, file processing, download batch input file, and download batch acknowledgement. Each batch step has 5 columns. The first 4 are labelled batch step, date, user ID, and status. An unlabelled 5th column contains buttons or pulldown menus for some of the entries. The file approval step has a pulldown menu labelled approve. The  download batch input file, and download batch acknowledgement steps each have a download button. After this is a payment transactions summary table that shows information about the payment totals for each currency. This includes the currency name, amount processed, amount to be processed, amount invalid, amount failed, amount schedules, amount waiting, and the total payment amount for that currency. After this is a record summary table showing the number of records processed, records to be processed, invalid payments, failed payments, and total records. This is followed by 3 buttons labelled refresh, batch list, and batch details.")

##### Accessing the Batch Overview page

Open the **Batch Overview** page from:

* The **View Batch** button on the **Upload Batch Jobs** page, after selecting **Select File** to upload the request file.
* The **Batch Overview** option from the job-specific action button on the **Batch Job Reports** page.

##### Understanding the page

The **Batch Overview** page includes the following sections:

* **Batch Step:** Shows the different stages of the job from ingestion through completion, with buttons for relevant actions.
* **Payment Transactions:** Shows currency-specific total payment amounts in terms of processing outcomes.
* **Record Summary:** Summarizes records included in the job in terms of processing outcomes.
* **Process Summary:** Summarizes processed operations that were included in the job.

The job and its status determine which sections show up:

* The **Payment Transactions** section shows up when the job includes payments.
* The **Process Summary** section shows up after the job is processed.

See the following definitions for more details about each section of the **Batch Overview** page.

##### The Batch Step section

The **Batch Step** section includes up to 7 rows from the following list:

* **File Upload**: Shows if the request file has been uploaded.
* **File Approval**: Shows if the job has been approved.
* **File Schedule**: Shows whether the job is supposed to be processed immediately or in the future.
* **File Processing**: Shows if the job has been processed.
* **`CANCELLED`**: Shows that the job was canceled prior to approval or processing.
* **Download Batch Input File**: Select this option to download the request file.
* **Download Batch Acknowledgement**: Select this option to download a file acknowledging that the request was uploaded.
* **Download Batch Error Acknowledgement**: Select this option to download a file acknowledging that the request couldn't be ingested due to errors.
* **Download Response File**: Select this option to download a response file for the job.

> **Note:** The job and its status determines which rows show up. Most rows will have a relevant action button.

After selecting **Approve**, details show up in the **File Approval** row. If the request was scheduled to be processed in the future it'll be mentioned in the **File Schedule** row, and the **Process** button won't show up until then. However, if the request is scheduled to be processed immediately then the request has the `IMMEDIATE` status and the **Process** button shows up immediately.

![Batch Steps](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-batchstep.png "The batch step section screen shows a table with 6 batch steps: file upload, file approval, file schedule, file processing, download batch input file, and download batch acknowledgement. Each batch step has 5 columns. The first 4 are labelled batch step, date, user ID, and status. An unlabelled 5th column contains buttons or pulldown menus for some of the entries. The file approval step has a pulldown menu labelled approve. The  download batch input file, and download batch acknowledgement steps each have a download button.")

Cancel a job by selecting **Cancel Batch** from the **Approve** or **Process** button's dropdown menu. The **Process** button shows up on the **File Processing** row when the request is approved, immediately or at a scheduled time, as long as there are no input errors.

![Batch, Approve Button](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-approvebutton.png "A pulldown menu button labelled approve, with a popup box that says cancel batch. The popup box has an x to close the box.")

Selecting **Process** starts the batch job. Depending on the batch processing queue, a **Pause** button may show up. Select the **Pause** button to set the job status to `STOPPED` and temporarily stop processing. When a job is `STOPPED`, the **Resume** button shows up in place of the **Pause** button. Select **Resume** to set the job status to `PROCESSING` and resume processing the job.

> **Note:** It may take a few minutes to complete processing. You need to select the **Refresh** button to get the latest data.

Download one of the following files when it is available by selecting the corresponding **Download** button:

* Input
* Request
* **Acknowledgement**
* **Acknowledgement Error**
* **Response**
* **Error**

![Batch Response Files](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-responsefiles.png "The batch overview screen shows the name of the file, followed by a link labelled batch step. There is a table with 6 batch steps: file upload, file approval, file schedule, file processing, download batch input file, and download batch acknowledgement. Each batch step has 5 columns. The first 4 are labelled batch step, date, user ID, and status. An unlabelled 5th column contains buttons or pulldown menus for some of the entries. The file upload, approval, schedule, and processing steps are completed. The download batch input file, download batch acknowledgement, download response file, and download response error file steps each have a download button.")

> **Note:** You can select the file format while downloading. Files are downloaded to the default download folder for your browser.

#### The Payment Transactions section

The **Payment Transactions** section only shows up if the request file includes any payment records. The table shows processing outcomes by currency and job status.

Each row in the **Payment Transactions** section shows data about the payments, organized by the type of currency. The data shows up in the following columns:

* **Currency:** The 3-letter currency code
* **Processed:** The amount that was successfully processed
* **To be Processed:** The amount that is yet to be processed
* **Invalid:** The amount that couldn't be processed due to being in an incorrect request format, such as a negative amount
* **Failed:** The amount that couldn't be processed due to processing errors
* **Scheduled:** The amount cleared for processing and queued to be processed by a scheduled job
* **Waiting:** The amount cleared for processing. This money is dispensed after a registered payment method is added to the payee's account, such as a bank account or card.
* **Total:** The total payment amount for that currency, independent of the processing outcome

> **Note:** Only currencies supported by your program show up.

![Batch Payment Transactions](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-paymenttransactions.png "The payment transactions summary table shows information about the payment totals for each currency. This includes the currency name, amount processed, amount to be processed, amount invalid, amount failed, amount schedules, amount waiting, and the total payment amount for that currency.")

Payments with an incorrect amount show up in the **Invalid** column.

When the records in the **Invalid** column are resolved, the total amount that can't be processed shows up in the **Failed** column.

The amount that shows up under **Waiting** shows that:

* The corresponding payments are cleared for processing.
* The payee's account can't receive money because it doesn't have a registered payment method, such as a bank account or card.

The total payment amount scheduled to be processed in the future shows up under **Scheduled**. After processing, the **Total** amount for the job will be identical to the **Processed** amount when:

* The current date and time is equal to or later than the scheduled date and time, or the job is scheduled to be processed immediately.
* All errors are resolved.
* The payee accounts have registered payment methods.

#### The Record Summary section

The **Record Summary** section provides a summary of records included in your batch job, organized by processing status. The data shows up in the following columns:

* **Processed Records:** Number of records in the job that were processed successfully
* **To be Processed Records:** Number of records in the job that aren't processed yet
* **Failed Records:** Number of records in the job that didn't complete successfully
* **Invalid Records:** Number of records in the job that aren't valid because of incorrect request formats
* **Pending Records:** Number of records in the job that are pending approval
* **Total Records:** Total number of records in the batch job

![Batch Record Summary](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-recordsummary.png "The record summary table shows the number of records processed, records to be processed, invalid payments, failed payments, and total records.")

When there are no processing errors, the number of **Processed Records** equals the number of **Total Records**.

#### The Process Summary section

The **Process Summary** section shows up after the job has been processed. The data shows up in the following columns:

* **Processed Operations:** Number of operations that were successfully processed
* **Failed Operations:** Number of failed operations
* **Scheduled/Waiting Operations:** Number of operations that are scheduled to be processed later or awaiting payment method registration. See **Payment Transactions**.
* **Total Operations:** Total number of operations included in the job for the operation type

![Batch Process Summary](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-processsummary.png "The batch process summary shows data about processed operations, failed operations, schedule operations, waiting operations, and total operations. There are summaries for profile, bank account, prepaid card, and payments.")

Assuming all errors were resolved and no operations are scheduled or waiting, the number of **Processed Operations** for a given operation type would be equal to the number of **Total Operations** for the same kind of operation.

#### Next steps

* Select the **Batch List** button to return to your most recent job report.
* Select the **Batch Details** button to see record-level details for the job.

### Using the Batch Details page

Look up information about a batch job's status by using the **Batch Details** page.

![Batch Details page](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-batchdetailspage.png "The batch results screen shows the batch name, the issuer, batch type, and creation date. There are pulldown fields for status and operation results. There is a text entry field for identifier. There are two buttons labelled search and reset. There is a list of payments for the batch, including the identifier, the operation results, and the status, with buttons to download each record detail. Each operation has a flag showing whether it was a success or failure. There are buttons labeled batch list and batch overview.")

#### Accessing the Batch Overview page

Open the **Batch Details** page from:

* The **Batch Details** button on the **Batch Overview** page.
* The **Batch Details** option from action button for that job on the **Batch Job Reports** page.

#### Understanding the page

By default, the page shows the batch details of all records included in the batch job. Filter the records using one or more of the following criteria:

* Record status
* The payee's unique identifier
* Operation results

The top-level rows on the **Batch Details** page show a record in the batch job that applies to a specific payee account. Expand a row to see the operations in that record. When a batch record fails before processing any of its operations, you won't be able to expand the row for that batch record.

See operation-level details by selecting the **Record Detail** button on the record row. Each payee account included in a record has a `FAILURE`, `SUCCESS`, or `PARTIAL` visual marker to highlight the overall processing results for that payee account.

> **Note:** Records can only be expanded on the **Batch Details** page if they have been processed, such as when the batch job status is `COMPLETED`. No rows show up for jobs that have the `INGESTING` status.

#### Operation outcomes

The following list defines the status options for an overall batch job:

| Job Status | Description |
| ---: | :--- |
| `PENDING` | The job is pending approval. |
| `APPROVED` | The job is approved and is queued for processing. |
| `BLOCKED` | The job is blocked due to system errors. |
| `PROCESSING` | The job is currently being processed. |
| `STOPPED` | Processing is halted for the job. |
| `CANCELLED` | The job was canceled prior to being processed. |
| `COMPLETED` | The job is processed. |
| `INGESTING` | The job is being ingested following upload. |
| `UNPARSABLE` | The job can't be parsed due to request format issues. |

The following list defines the status options for an individual record in a batch job:

| Record Status | Description |
| ---: | :--- |
| `COMPLETED` | The record was processed. |
| `PENDING` | The record is pending approval. |
| `INVALID` | The record can't be parsed due to request format issues. |
| `FAILED` | The record wasn't processed because of an error. |

The following list defines the operation results for an individual record in a batch job:

| Operation Status | Description |
| ---: | :--- |
| `SUCCESS` | All operations included in the record were processed successfully. |
| `PARTIAL SUCCESS` | Some operations included in the record were processed successfully. |
| `FAILURE` | All operations included in the record were processed unsuccessfully. |

### Using the Batch Record Detail page

Review operation-level details of an individual batch record using the **Batch Record Detail** page.

![Batch Record Detail page](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-batchrecorddetailspage.png "The batch record detail page has 2 tabs, profile and payment. The profile tab is selected. The page shows details that identify the batch record: first name, last name, and pay portal ID. Then there is an address section, followed by a preferences section that shows the payee's preferred contact method. There is a button labelled return to batch details.")

#### Accessing the Batch Record Detail page

Open the **Batch Record Detail** page by selecting the corresponding **Record Detail** button on the **Batch Details** page.

#### Understanding the page

The **Batch Record Detail** page shows a tab for each operation in the request. Each individual operation has a visual marker that shows its processing outcome, similar to the **Batch Details** page:

* Green tick indicates the operation was successfully processed.
* Red cross indicates the operation wasn't successful.
* Blue clock indicates the operation is waiting because the payee account doesn't have a registered payment method and can't receive money.
* No icon indicates the operation couldn't or hasn't been processed yet. This applies to batch jobs that don't have a `COMPLETED` status.

Records that couldn't or haven't been processed don't have visual markers.

![Batch Record Detail tabs](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-batchrecorddetailstabs.png "The batch record detail page has 2 tabs, profile and payment. The profile tab is selected.")

> **Note:** The page only shows tabs for the operations included in the record.

Select a tab to reveal details about that operation, including errors.

![Batch Record Detail page with warnings](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-batchrecorddetailserrors.png "The batch record detail page has 2 tabs, profile and payment. Each has a red flag with a white x that indicates failure. The profile tab is selected. There are 2 messages warning that data requirements aren't met, and that there needs to be a first name in the first name field. The page shows details that identify the batch record: last name, pay portal ID, and owner type. Then there is an address section, followed by a preferences section that shows the payee's preferred contact method. There is a button labelled return to batch details.")

### Using the Batch Job Reports page

Get a report of past batch jobs using the **Batch Job Reports** page.

![Batch Job Reports page](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-jobreportspage.png "The batch job reports screen has a button to choose a program for the batch job, pulldown menus for start date, end date, status, and batch type. There is a text entry field labelled batch name. The start and end date fields have a calendar icon, and note saying they are in Greenwich Mean Time. After this are 2 buttons labelled search and reset. There is a list of batch files that show the batch type, program name, domain, batch name, batch status, number of records in the batch, date uploaded, date scheduled, and date processed. Each batch has either an action button, or a pulldown button labelled approve.")

#### Accessing the Batch Record Detail page

Open the **Batch Record Detail** page by selecting **Batch Processing** in the left menu pane of the Client Portal. You can also select **Batch Processing > Batch Job Reports**.

![Batch Record Detail page](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-batchrecorddetailmenu.png "The batch processing pulldown menu shows 2 options, upload batch jobs, and batch jobs report.")

#### Understanding the page

Search for jobs in the **Batch Job Reports** page based on the following criteria:

* Program
* Job start date and time
* Job end date and time
* Job status. See the **Job Report columns** section for more details.
* Batch type

Jobs matching your filter criteria show up on the page, along with available actions for individual jobs. To generate a batch report:

1.	Select **Choose A Program** in the dropdown list.
2.	In the pop-up that shows up, enter the intended program or sub-program name in the **Filter** field to filter it, then select it. Alternatively, browse to the program and sub-program from the treeview and select it.
3.	Select the **Start Date** that includes your intended batch jobs. You can also select a specific time by selecting the clock icon in the calendar pop-up. To return to the calendar, select the calendar icon in the clock pop-up.
4.	Select the **End Date** that includes your intended batch jobs.
5.	Select the **Status** of the intended jobs. Available statuses are:

| Job Status | Description |
| ---: | :--- |
| `All` | All jobs irrespective of status |
| `PENDING` | Jobs that are pending approval |
| `APPROVED` | Jobs that have been approved and are queued for processing |
| `BLOCKED` | Jobs that have been blocked due to system errors |
| `PROCESSING` | Jobs that are currently being processed |
| `STOPPED` | Jobs that were paused while being processed |
| `CANCELLED` | Canceled jobs |
| `COMPLETED` | Jobs that finished processing |
| `INGESTING` | Jobs that are currently being ingested following upload |
| `UNPARSABLE` | Jobs that couldn't be processed due to errors in the request file |

6.	Select the **Batch Type**.
7.	Select **Search**. A list of matching jobs shows up.

Refer to the following section for details on the information presented. If you want to clear your current filter and start again, select **Reset** and repeat the preceding steps with your desired filtering criteria.

#### Job Report columns

A job report consists of the following columns:

* **Batch Type:** The batch type for a given job
* **Program Name:** The program or sub-program the job was applied to
* **Domain:** The client domain or sub-domain
* **Batch Name:** The name of the request file for the corresponding job. See **Uploading a request file**.
* **Status:** The current status of the job
* **Records:** The total number of records included in the job
* **Uploaded:** The date and time that the request file for the job was uploaded
* **Scheduled:** The date and time that the job was scheduled for processing. This applies to scheduled jobs.
* **Processed:** The date and time that the job was processed. This applies to processed jobs. When none of the jobs in the following screenshot have been processed yet, this column is empty.

![Batch Job Report columns](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-batchjobreportscolumn.png "The batch job reports table has a list of batch files that show the batch type, program name, domain, batch name, batch status, number of records in the batch, date uploaded, date scheduled, and date processed. Each batch has an action button.")

#### Job sorting and navigation options

Sort values in ascending or descending order by selecting the upward or downward arrow that shows up on a column header. By default, the **Batch Job Reports** page shows a maximum of 20 matching jobs. You can use the page navigation buttons to show more jobs, or increase the number of matching jobs to show on the page to 50 or 100. The total number of matching batch jobs shows up in the table header. See the following screenshot:

![Job sorting and navigation](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-jobsortingnavigation.png "The job sorting interface shows the number of pages, 1 of 1, with a pulldown menu with the option to select twenty, fifty, or one hundred jobs per page. The twenty option is selected. There are navigations buttons with arrows that control how many records you can advance or rewind in the report. A number 1 shows how many reports on the current page.")

#### Viewing job summaries

Hovering the cursor on a **Batch Name** value opens a pop-up with the **Record Summary** and **Amount Summary** for the corresponding job. The job determines which details show up in the summary. For example, jobs with no payments won't have an **Amount Summary**. To avoid visual clutter, "Multiple currencies" shows up under **Amount Summary** when a job includes amounts in two or more currencies.

#### Job-specific actions

Perform a job-specific action using the corresponding button in the last column. Select the button's dropdown icon and select one of the actions that shows up, as shown in the following screenshots. Certain actions, such as **Approve** or **Process**, make the color of the button change to blue. Complete one of these actions by selecting the corresponding button.

> **Note:** Regardless of button color, the job and its status determine which  actions are available.

![Job-specific actions](https://docs.hyperwallet.com/assets/docs/pay-portal-admin/onebatch/batch-jobspecificactions.png "There is a job marked as immediate, with a date and time, and a pulldown menu labelled action. The pulldown menu shows options for batch overview, batch details, download batch input file, download batch acknowledgement, download response file, and download response error file.")

The following table lists all possible actions and shows whether they open a dropdown menu:

| Action | Dropdown menu | Description |
| :--- | :--- | :--- |
| **Approve** | No | Approves the job for processing. |
| **Process** | No | Starts processing the job. |
| **Batch Overview** | Yes | Opens the **Batch Overview** page for the job. |
| **Batch Details** | Yes | Opens the **Batch Details** page for the job. |
| **Cancel Batch** | Yes | Cancels the job. |
| **Download Batch Input File** | Yes | Downloads the request file. |
| **Download Batch Acknowledgement** | Yes | Downloads the batch acknowledgement file. |
| **Download Batch Error Acknowledgement** | Yes | Downloads the batch acknowledgement error file. |
| **Download Response File** | Yes | Downloads the response file. |
| **Download Response Error File** | Yes | Downloads the error file. |
