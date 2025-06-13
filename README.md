# Exchange EWS and SMTP Relay Usage Scanner

![Exchange](https://img.shields.io/badge/Exchange-2013%2F2016%2F2019-blue)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)

A PowerShell script that identifies applications and tools using Exchange Web Services (EWS) or on-premise Exchange as an SMTP relay. The script generates a detailed HTML report to help with migration planning and application inventory.

![Sample Report](https://placeholder.svg?height=300&width=600&query=Sample+Exchange+EWS+Scanner+HTML+Report)

## 🚀 Features

- **EWS Usage Detection**: Identifies applications using Exchange Web Services
- **SMTP Relay Detection**: Discovers applications using on-premise Exchange as a mail relay
- **Detailed Reporting**: Generates a comprehensive HTML report with application details
- **Historical Analysis**: Configurable time range for log analysis
- **Low Impact**: Designed to run with minimal performance impact on production servers

## 📋 Prerequisites

- On-premise Exchange Server (2013, 2016, 2019)
- Exchange Management Shell
- Administrator privileges on the Exchange server
- Access to IIS logs, Exchange logs, and message tracking logs

## 📥 Installation

1. Download the script from this repository
2. Save it to your Exchange server
3. No additional modules are required beyond the standard Exchange Management Shell

## 🔧 Usage

Run the script from Exchange Management Shell:

```powershell
.\Get-ExchangeUsageReport.ps1
