# PowerShell TOTP Generator

A PowerShell implementation of the Time-Based One-Time Password (TOTP) algorithm (RFC 6238) for generating short-lived authentication codes.

## Features

- Implements RFC 6238 TOTP standard (HMAC-SHA1 variant)
- Supports Base32-encoded secrets
- Configurable code length (typically 6-8 digits)
- Adjustable time window (default 30-second intervals)
- Compatible with most TOTP-based authentication systems

## Prerequisites

- Windows PowerShell 2.0 or newer
- .NET Framework 3.5 or newer

## Installation

1. Clone this repository or download the script:

    ```
    git clone https://github.com/gamelton/powershell-totp.git
    ```

2. Import the script into your PowerShell session:

    ```
    . .\totp.ps1
    ```

## Usage

### Basic Syntax

```
Get-Otp [-SECRET] <String> [-LENGTH] <Int32> [-WINDOW] <Int32>
```

### Parameters

| Parameter | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| SECRET    | Base32-encoded secret key (case-insensitive)                               |
| LENGTH    | Number of digits in OTP (typically 6 or 8)                                 |
| WINDOW    | Time step window in seconds (standard implementations use 30)             |

### Examples

**Generate a 6-digit code with 30-second window:**

```
Get-Otp -SECRET "JBSWY3DPEHPK3PXP" -LENGTH 6 -WINDOW 30
```

**Generate an 8-digit code with 60-second window:**

```
Get-Otp -SECRET "ABCDEFG23456ABCD" -LENGTH 8 -WINDOW 60
```

**Store secret securely and generate code:**

```
$secureSecret = Read-Host -AsSecureString
$secret = [Runtime.InteropServices.Marshal]::PtrToStringAuto([Runtime.InteropServices.Marshal]::SecureStringToBSTR($secureSecret))
Get-Otp -SECRET $secret -LENGTH 6 -WINDOW 30
```

## Acknowledgements

- RFC 6238: TOTP Specification
- RFC 4226: HOTP Specification
- Initial implementation by Jon Friesen (2015)
