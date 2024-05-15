# config-dhcp-failover
```


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
