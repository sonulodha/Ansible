# Preparing Microsoft Windows Hosts for Automation

# Minimum Requirements

Managed hosts need the following minimum base requirements:

    • Windows Server (2008, 2008 R2, 2012, 2012 R2, 2016, or 2019) or Windows 7, 8.1, or 10
    • PowerShell 3.0 or newer
    • .NET Framework 4.0 or newer


# Important
    Due to a WinRM memory issue, PowerShell 3.0 requires a hotfix. Refer to the Microsoft support article available 
    at https://support.microsoft.com/en-us/help/2842230/out-of-memory-error-on-a-computer-that-has-a-customizedmaxmemorypersh 
    for more information.

Install the latest stable updates to keep your systems secure and reliable

# Configuring Windows for Ansible Access

    • Ansible communicates with Windows hosts using Windows Remote Management. WinRM is a Microsoft implementation of the 
      SOAP-based WS-Management standard protocol and provides a noninteractive login to control a remote system.

    • WinRM is enabled by default since Windows Server 2012. However, you still need to configure a WinRM listener, the
      corresponding firewall rules, and the authentication mechanism.

    • Ansible uses the PowerShell Remoting Protocol (PSRP) on top of WinRM to execute PowerShell commands on a target.
      PSRP provides a faster direct connection to PowerShell.

    • Since the Ansible connection normally depends on both WinRM and PowerShell, Ansible cannot interact directly with WinRM
      listeners or upgrade PowerShell.

# Configuring for Development Environments

The Ansible project provides an example PowerShell script for configuring Windows managed hosts for remote access. This script is
designed for use in lab and development environments where high levels of security are not a concern. Ansible does not recommend 
using the example script in production environments due to the potential weakening of the authentication mechanism.

Find the script in the official repository 

      https://github.com/sonulodha/ansible/blob/main/examples/scripts/ConfigureRemotingForAnsible.ps1

      https://github.com/ansible/ansible/blob/devel/examples/scripts/ConfigureRemotingForAnsible.ps1. ( official) 

The ConfigureRemotingForAnsible.ps1 script performs the following actions.

     1. Confirms PowerShell version 3 or higher is installed.
     2. Runs the WinRM service, if not already running, and configures it to automatically start on boot.
     3. Enables PowerShell Remoting and an SSL listener.
     4. Sets the LocalAccountTokenFilterPolicy registry key to 1.
     5. Optionally configures basic authentication or CredSSP. This is discussed in detail below.
     6. Configures the Windows firewall for WinRM connections over both HTTP and HTTPS.

Run ConfigureRemotingForAnsible.ps1 as an Administrator with the appropriate options for your environment.we are uses  the
  
    -DisableBasicAuth and -EnableCredSSP options as a security preference.

    ConfigureRemotingForAnsible.ps1 also creates a self-signed  certificate for HTTP

    ConfigureRemotingForAnsible.ps1 also creates a self-signed certificate for HTTPS communication. 

Several options exist to customize the SSL certificate or force the creation of a new one





# The following list describes the list of arguments that you can use with the PowerShell script:

ConfigureRemotingForAnsible.ps1 Argument List

    -EnableCredSSP 
Enables the CredSSP authentication protocol.)

    -DisableBasicAuth 
Disables Basic auth. This option is recommended since Basic auth is the least secure WinRM auth method.

    -CertValidityDays 
Specifies the expiration of the self-signed SSL certs created for HTTPS. The default validity is 1095 days 3 years.

    -ForceNewSSLCert
Forces the creation of a new SSL certificate.

    -SubjectName
Specifies the CN (Common Name) of the SSL certificate. Defaults to the host name.

    -SkipNetworkProfileCheck 
Allows for enabling PS Remoting without checking the network profile.

    -Verbose
Enables verbose output. This option is useful for debugging.


