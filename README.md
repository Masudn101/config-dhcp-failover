Configuring DHCP failover on Windows Server involves several steps. Below is a PowerShell script that automates these steps:

```powershell
# Define parameters for DHCP failover
$PrimaryServerName = "PrimaryDHCP"
$PrimaryServerIP = "192.168.1.10"
$SecondaryServerName = "SecondaryDHCP"
$SecondaryServerIP = "192.168.1.11"
$ScopeName = "MyScope"
$FailoverName = "MyFailover"
$FailoverMode = "HotStandby"
$MaximumClientLeadTime = "1.00:00:00"
$StateSwitchoverInterval = "00:10:00"
$SharedSecret = "MySharedSecret"

# Import DHCP module
Import-Module DHCP

# Create primary DHCP server
Add-DhcpServerInDC -DnsName $PrimaryServerName -IPAddress $PrimaryServerIP

# Create secondary DHCP server
Add-DhcpServerInDC -DnsName $SecondaryServerName -IPAddress $SecondaryServerIP

# Configure DHCP failover
Add-DhcpServerv4Failover -Name $FailoverName -ScopeId $ScopeName `
    -PrimaryServer $PrimaryServerName -SecondaryServer $SecondaryServerName `
    -MaximumClientLeadTime $MaximumClientLeadTime -StateSwitchInterval $StateSwitchoverInterval `
    -SharedSecret $SharedSecret -Mode $FailoverMode

# Verify DHCP failover configuration
Get-DhcpServerv4Failover -Name $FailoverName
```

This script first defines parameters such as server names, IP addresses, scope name, failover name, failover mode, maximum client lead time, state switchover interval, and shared secret. Then it imports the DHCP module and adds the primary and secondary DHCP servers. Finally, it configures DHCP failover with the specified parameters and verifies the configuration.

Make sure to replace the placeholders (`$PrimaryServerName`, `$PrimaryServerIP`, `$SecondaryServerName`, `$SecondaryServerIP`, `$ScopeName`, `$FailoverName`, `$MaximumClientLeadTime`, `$StateSwitchoverInterval`, and `$SharedSecret`) with your actual values.

Save the script with a `.ps1` extension and execute it on your Windows Server with appropriate administrative privileges.
