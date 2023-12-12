PARAM(
    [string] [Parameter(Mandatory = $True, HelpMessage = "Choose subscription you want be inventored")] $SubscriptionName
    )


#Login to Azure
Connect-AzAccount
 
#Select Azure Subscription
Get-AzSubscription -SubscriptionName $SubscriptionName | Select-AzSubscription
 
#Collect Data
$AzureSQLBackupInventory = @()
$AzureSQLServers = Get-AzResource  | Where-Object ResourceType -EQ Microsoft.SQL/servers
foreach ($AzureSQLServer in $AzureSQLServers){
    $AzureSQLServerDataBases = Get-AzSqlDatabase -ServerName $AzureSQLServer.Name -ResourceGroupName $AzureSQLServer.ResourceGroupName | Where-Object DatabaseName -NE "master"
        foreach ($AzureSQLServerDataBase in $AzureSQLServerDataBases) {
            $DBLevelInventory =  @()
            $BackupState = Get-AzSqlDatabaseGeoBackupPolicy  -ServerName $($AzureSQLServerDataBase.ServerName) -DatabaseName $($AzureSQLServerDataBase.DatabaseName) -ResourceGroupName $($AzureSQLServerDataBase.ResourceGroupName) | Select-Object -ExpandProperty State
            echo $BackupState
                        
        }
}


