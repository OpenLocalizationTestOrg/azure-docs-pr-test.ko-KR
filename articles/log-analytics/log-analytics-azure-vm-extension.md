---
title: "Azure 가상 컴퓨터 tooLog aaaConnect 분석 | Microsoft Docs"
description: "Windows 및 Linux 용 Azure에서 실행 중인 가상 컴퓨터, hello 방식으로 수집 된 로그의 좋으며 메트릭은 hello 로그 분석 Azure VM 확장을 설치 합니다. Hello Azure 포털 또는 PowerShell tooinstall hello Azure Vm에 가상 컴퓨터 확장 로그 분석을 사용할 수 있습니다."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Azure 가상 컴퓨터 tooLog 분석 로그 분석 에이전트를 사용 하 여 연결

Windows 및 Linux 컴퓨터에 대 한 hello 권장 되는 로그를 수집 하는 방법 및 메트릭을 hello 로그 분석 에이전트를 설치 하는 것입니다.

hello 가장 쉬운 방법은 tooinstall hello 로그 분석 Azure 가상 컴퓨터 에이전트가 hello 로그 분석 VM 확장을 통해 수행 됩니다.  Hello 확장을 사용 하 여 hello 설치 프로세스를 간소화 하 고 자동으로 hello 에이전트 toosend 데이터 toohello 로그 분석 작업 영역 사용자가 지정한를 구성 합니다. hello 에이전트를 확보 하는 hello 최신 기능 및 수정 사항 자동으로 업그레이드도 됩니다.

Hello를 사용 하면 Windows 가상 컴퓨터에 대 한 *Microsoft Monitoring Agent* 가상 컴퓨터 확장.
Hello를 사용 하면 Linux 가상 컴퓨터에 대 한 *OMS 에이전트에 대 한 Linux* 가상 컴퓨터 확장.

에 대 한 자세한 내용은 [Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 및 hello [Linux 에이전트](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

로그 데이터에 대 한 에이전트 기반 컬렉션을 사용 하는 경우 구성 해야 [로그 분석에서 데이터 원본을](log-analytics-data-sources.md) toospecify hello 로그 및 toocollect 메트릭을 합니다.

> [!IMPORTANT]
> 사용 하 여 로그 분석 tooindex 로그 데이터를 구성 하는 경우 [Azure 진단](log-analytics-azure-storage.md), hello 로그가 두 번 수집 된 다음 로그 동일 hello 에이전트 toocollect hello를 구성 합니다. 두 데이터 원본 모두에 대해 청구됩니다. Hello 에이전트가 설치 되어 있는 경우 hello 담당자만을 사용 하 여 로그 데이터를 수집 하-Azure 진단의 로그 분석 toocollect 로그 데이터를 구성 하지 마십시오.
>
>

세 가지가 쉽게 tooenable hello 로그 분석 가상 컴퓨터 확장입니다.

* Hello Azure 포털을 사용 하 여
* Azure PowerShell 사용
* Azure Resource Manager 템플릿을 사용하여

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>Hello Azure 포털에서에서 VM 확장 hello를 사용 하도록 설정
로그 분석에 대 한 hello 에이전트를 설치 하 고 hello hello를 사용 하 여 실행 되는 Azure 가상 컴퓨터를 연결할 수 [Azure 포털](https://portal.azure.com)합니다.

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall hello 로그 분석 에이전트 및 로그 분석 작업 영역을 tooa hello 가상 컴퓨터를 연결 합니다.
1. Hello에 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. 선택 **찾아보기** hello에 왼쪽의 hello, 포털 및 이동한 다음 너무**로그 분석 (OMS)** 선택 합니다.
3. 로그 분석 작업 영역을 목록에서 Azure VM hello로 toouse 원하는 hello 하나를 선택 합니다.  
   ![OMS 작업 영역](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. **Log Analytics 관리**에서 **가상 컴퓨터**를 클릭합니다.  
   ![가상 컴퓨터](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. Hello 목록이 **가상 컴퓨터**, 선택 hello tooinstall hello 에이전트 원하는 가상 컴퓨터. hello **OMS 연결 상태** hello VM 한다는 나타냅니다는 **연결 되어 있지 않은**합니다.  
   ![연결되지 않은 VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. 가상 컴퓨터에 대 한 hello 측면에서 선택 **연결**합니다. hello 에이전트가 자동으로 설치 되 고 로그 분석 작업 영역에 대해 구성 합니다. 이 프로세스는 몇 분만, hello OMS 연결 상태는이 시간 동안 *연결 하는 중...*  
   ![VM 연결](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. 설치 하 고 hello 에이전트 연결 후 hello **OMS 연결** 상태는 업데이트 된 tooshow 됩니다 **이 작업 영역**합니다.  
   ![연결됨](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>PowerShell을 사용 하 여 hello VM 확장을 사용 하도록 설정
Tooprovide hello PowerShell을 사용 하 여 가상 컴퓨터를 구성할 때 필요한 **workspaceId** 및 **workspaceKey**합니다. json 구성에서 hello 속성 이름에는 **대/소문자 구분**합니다.

Id hello 및 hello에 키를 찾을 수 있습니다 **설정을** hello OMS 포털의 페이지나 hello 앞 예제에에서 나와 있는 것 처럼 PowerShell을 사용 하 여 합니다.

![작업 영역 ID 및 기본 키](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Azure 클래식 가상 컴퓨터와 Resource Manager 가상 컴퓨터에 대한 명령이 서로 다릅니다.  다음은 클래식 및 Resource Manager 가상 컴퓨터의 예제입니다.

클래식 가상 컴퓨터에 대 한 hello 다음 PowerShell 예제를 사용 합니다.

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

CLI 다음 hello를 사용 하 여 Linux vm의 리소스 관리자
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

리소스 관리자 가상 컴퓨터에 대 한 hello 다음 PowerShell 예제를 사용 합니다.

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a>서식 파일을 사용 하 여 hello VM 확장 배포
Azure 리소스 관리자를 사용 하 여 hello 배포 및 응용 프로그램의 구성을 정의 하는 JSON 형식으로 서식 파일을 만들 수 있습니다. 이 서식 파일 리소스 관리자 템플릿을 라고 하 고 선언적으로 toodefine 배포를 제공 합니다. 서식 파일을 사용 하 여 hello 앱 수명 주기 전체에서 응용 프로그램을 배포 하 고 것을 확신할 리소스 일관 된 상태에서 배포 되 고 반복 해 서 있습니다.

Hello 로그 분석 에이전트를 포함 하 여 리소스 관리자 템플릿의 일환으로, 각 가상 컴퓨터는 미리 구성 된 tooreport tooyour 로그 분석 작업 영역을 확인할 수 있습니다.

리소스 관리자 템플릿에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)을 참조하세요.

다음은 Windows hello 설치 된 Microsoft Monitoring Agent 확장을 실행 하는 가상 컴퓨터를 배포 하는 데 사용 되는 리소스 관리자 템플릿의 예입니다. 이 서식 파일은 일반적인 가상 컴퓨터 템플릿을 추가 수행 하는 hello로:

* workspaceId 및 workspaceName 매개 변수
* Microsoft.EnterpriseCloud.Monitoring 리소스 확장 섹션
* 출력 toolook hello workspaceId 및 workspaceSharedKey를

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

다음 PowerShell 명령을 hello를 사용 하 여 서식 파일을 배포할 수 있습니다.

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Hello 로그 분석 VM 확장 문제 해결
일반적으로 Azure Portal 또는 Azure PowerShell 중 하나에서 무엇인가 작동하지 않을 경우 메시지가 표시됩니다.

1. Hello에 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. Hello VM 찾아서 VM 세부 정보를 엽니다.
3. 클릭 **확장** toocheck OMS 확장은 사용 하는지 여부입니다.

   ![VM 확장 보기](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Hello 클릭 *MicrosoftMonitoringAgent*(Windows) 또는 *OmsAgentForLinux*(Linux) 확장 및 뷰 세부 정보입니다. 

   ![VM 확장 세부 정보](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Windows Virtual Machines 문제 해결
경우 hello *Microsoft Monitoring Agent* VM 에이전트 확장은 설치 하지 않는 또는 보고를 hello tootroubleshoot hello 문제 단계를 따라 수행할 수 있습니다.

1. Hello Azure VM 에이전트가 설치 되어 있고 올바르게 hello를 사용 하 여 작업의 단계를 하는 경우 확인 [KB 2965986](https://support.microsoft.com/kb/2965986#mt1)합니다.
   * Hello VM 에이전트 로그 파일을 검토할 수 있습니다.`C:\WindowsAzure\logs\WaAppAgent.log`
   * Hello 로그가 없는 경우에 hello VM 에이전트가 설치 되지 않았습니다.
     * [클래식 Vm에 hello Azure VM 에이전트를 설치 합니다.](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Microsoft Monitoring Agent 확장 하트 비트 작업이 실행 되 고 단계를 수행 하는 hello를 사용 하 여 hello를 확인 합니다.
   * Toohello 가상 컴퓨터에 로그인
   * 작업 스케줄러를 열고 hello `update_azureoperationalinsight_agent_heartbeat` 작업
   * Hello 작업 활성화 되어 실행 되 고 1 분 간격 확인
   * Hello 하트 비트 로그 파일에서 확인 필요`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Hello Microsoft 모니터링 에이전트 VM 확장 로그 파일을 검토 합니다.`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Hello 가상 컴퓨터에서 PowerShell 스크립트를 실행할 수 있는지 확인
5. C:\Windows\temp 권한이 변경되지 않았는지 확인합니다.
6. Hello hello 가상 컴퓨터에서 다음 관리자 권한 PowerShell 창에서 명령을 입력 하 여 hello Microsoft Monitoring Agent의 hello 상태 보기`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Hello에 Microsoft Monitoring Agent 설치 로그 파일을 검토`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

자세한 내용은 [Windows 확장 문제 해결](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.

### <a name="troubleshooting-linux-virtual-machines"></a>Linux Virtual Machines 문제 해결
경우 hello *Linux 용 OMS 에이전트* VM 에이전트 확장은 설치 하지 않는 또는 보고를 hello tootroubleshoot hello 문제 단계를 따라 수행할 수 있습니다.

1. Hello 확장 상태 이면 *알 수 없는* hello Azure VM 에이전트가 설치 되어 있는지 확인 하 고 hello VM 에이전트 로그 파일을 검토 하 여 제대로 작동`/var/log/waagent.log`
   * Hello 로그가 없는 경우에 hello VM 에이전트가 설치 되지 않았습니다.
   * [Linux Vm에 hello Azure VM 에이전트를 설치 합니다.](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Linux VM 확장에 대 한 검토 hello OMS 에이전트 로그 파일 기타 비정상 상태에 대 한 `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` 및`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Hello 확장 상태가 양호한 지 되지만 데이터 업로드 되지 않으면 Linux 로그 파일에 대 한 hello OMS 에이전트를 검토 합니다.`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>다음 단계
* 구성 [로그 분석에서 데이터 원본을](log-analytics-data-sources.md) toospecify hello 로그 및 메트릭 toocollect 합니다.
* 가상 컴퓨터에서 toogather 데이터 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.
* Azure에서 실행 중인 다른 리소스에 대해 [Azure Diagnostics를 사용하여 데이터를 수집](log-analytics-azure-storage.md) 합니다.

Azure에 없는 컴퓨터에 대 한 hello 다음 문서에서에서 설명 하는 hello 방법을 사용 하 여 hello 로그 분석 에이전트를 설치할 수 있습니다.

* [Windows 컴퓨터 tooLog 분석 연결](log-analytics-windows-agents.md)
* [Linux 컴퓨터 tooLog 분석 연결](log-analytics-linux-agents.md)
