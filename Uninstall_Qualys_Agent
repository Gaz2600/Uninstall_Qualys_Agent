$Services = @('DHCP','EventLog','lmhosts','TimeBrokerSvc','iphlpsvc','WinHttpAutoProxySvc','netprofm','NlaSvc')
$SRVCNAME = Get-Service $Services | where {$_.status -eq 'Running'}
$FinalSRVC = $SRVCNAME[2].Name

Foreach ($Service in $FinalSRVC) {

$SRVC = Get-Service $Service
Stop-Service -Name $SRVC.Name -Force

$args = "Uninstall=TRUE Force=TRUE"
New-Item -Path "C:\Program Files" -Name "_QualysUninstall" -ItemType "directory" 
Copy-Item -Path "C:\Program Files\Qualys\QualysAgent\Uninstall.exe" -Destination "C:\Program Files\_QualysUninstall" -Force
Start-Process -FilePath "C:\Program Files\_QualysUninstall\Uninstall.exe" -ArgumentList $args -Wait 
Remove-Item -Path "C:\Program Files\_QualysUninstall" -Recurse -Force
}

Foreach ($Service in $FinalSRVC) {

$SRVC = Get-Service $Service
Start-Service -Name $SRVC.Name

}
