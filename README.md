# Exchange EWS and SMTP Relay Usage Scanner

![Exchange](https://img.shields.io/badge/Exchange-2013%2F2016%2F2019-blue)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)

A PowerShell script that identifies applications and tools using Exchange Web Services (EWS) or on-premise Exchange as an SMTP relay. The script generates a detailed HTML report to help with migration planning and application inventory.


## 🚀 Features

- **EWS Usage Detection**: Identifies applications using Exchange Web Services
- **SMTP Relay Detection**: Discovers applications using on-premise Exchange as a mail relay
- **Detailed Reporting**: Generates a comprehensive HTML report with application details
- **Interactive File Dialogs**: Choose where to save reports and locate log files via GUI dialogs
- **Flexible Log Paths**: Automatically detects or allows manual selection of log locations
- **Progress Indicators**: Visual feedback during long-running operations
- **Detailed Logging**: Comprehensive output for troubleshooting
- **Error Resilience**: Robust error handling to prevent script failures

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

\`\`\`powershell
.\Get-ExchangeUsageReport.ps1
\`\`\`

### Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `-DaysToAnalyze` | Number of days of logs to analyze | 30 |
| `-UseFileDialog` | Show file dialogs to choose where to save the report and locate logs | $true |
| `-OutputPath` | Path where the HTML report will be saved (if not using dialog) | Desktop |
| `-IncludeMessageTracking` | Whether to include message tracking logs | $true |
| `-IISLogPath` | Specify the path to IIS logs directly (bypasses automatic detection) | Auto-detected |

### Examples

Basic usage with interactive dialogs:
\`\`\`powershell
.\Get-ExchangeUsageReport.ps1
\`\`\`

Specify a custom IIS log path (useful when logs are on a different drive):
\`\`\`powershell
.\Get-ExchangeUsageReport.ps1 -IISLogPath "D:\IISLogs\W3SVC1"
\`\`\`

Non-interactive mode with specific paths (useful for scheduled tasks):
\`\`\`powershell
.\Get-ExchangeUsageReport.ps1 -UseFileDialog $false -OutputPath "C:\Reports\EWSReport.html" -IISLogPath "D:\IISLogs\W3SVC1"
\`\`\`

Analyze a longer time period:
\`\`\`powershell
.\Get-ExchangeUsageReport.ps1 -DaysToAnalyze 60
\`\`\`

## 📊 Report Details

The HTML report contains two main sections:

### EWS Applications Tab
- Client IP addresses
- User agent strings (application identifiers)
- First and last seen timestamps
- Request count
- Common endpoints accessed

### SMTP Relay Applications Tab
- Client IP addresses
- First and last seen timestamps
- Message count
- Common sender addresses
- Authentication types used

## 🔍 How It Works

The script collects data from multiple sources:

1. **For EWS Usage**:
   - IIS logs for EWS endpoints (automatically detected or user-selected)
   - Exchange Web Services event logs
   - User agent analysis

2. **For SMTP Relay Usage**:
   - Message tracking logs
   - SMTP protocol logs
   - Authentication patterns

### Log Path Detection

The script uses a multi-layered approach to find the correct log paths:

1. First tries to use the path provided via `-IISLogPath` parameter (if specified)
2. Then attempts to detect the path from IIS configuration using the WebAdministration module
3. Falls back to the default path (`%SystemDrive%\inetpub\logs\LogFiles\W3SVC1`)
4. If logs aren't found and `-UseFileDialog` is enabled, prompts the user to select the correct folder
5. Continues with other data sources if IIS logs can't be located

### Progress Indicators

The script now provides detailed progress indicators:

- Shows which file is currently being processed
- Displays progress bars for long-running operations
- Reports the number of entries found at each step
- Provides detailed status messages throughout execution

## 🛠️ Troubleshooting

### Common Issues

**Script fails to load Exchange PowerShell modules**
- Ensure you're running from Exchange Management Shell
- Verify you have administrator privileges

**Missing data in the report**
- Check log retention settings on your Exchange server
- Verify the script has access to log directories
- Use the `-IISLogPath` parameter to specify the correct IIS log path

**Script runs slowly**
- Reduce the `-DaysToAnalyze` parameter
- Run with `-IncludeMessageTracking $false`

**IIS logs not found**
- Use the interactive dialog to browse to the correct location
- Specify the path directly with `-IISLogPath "D:\path\to\logs\W3SVC1"`
- Check if logs are being written to a non-default location

**Script appears to hang**
- Check the console for detailed progress messages
- The script now shows verbose output at each stage
- Processing large log files can take time, especially with many days of data

## 📋 Script Output Guide

The script provides detailed output to help track progress and troubleshoot issues:

- **Green text**: Success messages and completed operations
- **Yellow text**: Informational messages and warnings
- **Red text**: Error messages that require attention
- **Progress bars**: Visual indicators for long-running operations

## ⚠️ Limitations

- The script identifies applications primarily by IP address and user agent
- Some applications may use generic user agents that are difficult to identify
- The script does not detect EWS usage through load balancers without additional configuration
- Performance depends on the volume of logs and the specified time range

## 🔄 Version History

- **1.2.0** (2023-06-15): Added enhanced error handling, progress indicators, and fixed file dialog issues
- **1.1.0** (2023-06-14): Added flexible IIS log path detection and file dialogs
- **1.0.0** (2023-06-13): Initial release

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Contact

If you have any questions or feedback, please open an issue on this repository.

---

**Note**: This script is provided as-is without warranty. Always test in a non-production environment first.
