---
title: "Windows 가상 컴퓨터 크기 집합 aaaAutoscale | Microsoft Docs"
description: "Azure PowerShell을 사용하여 Windows 가상 컴퓨터 확장 집합 자동 크기 조정 설정"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a>가상 컴퓨터 확장 집합에서 자동으로 컴퓨터 크기 조정
가상 컴퓨터 크기 집합에 더 쉽게 있습니다 toodeploy 고 집합으로 동일한 가상 컴퓨터를 관리 합니다. 규모 집합은 대규모 응용 프로그램에 대한 높은 확장성과 사용자 지정 가능한 계산 계층을 제공하고 Windows 플랫폼 이미지, Linux 플랫폼 이미지, 사용자 지정 이미지 및 확장을 지원합니다. 규모 집합에 대한 자세한 내용은 [가상 컴퓨터 규모 집합](virtual-machine-scale-sets-overview.md)을 참조하세요.

이 자습서의 Windows 컴퓨터와 가상 컴퓨터 자동으로 크기 조정 hello hello에 크기 집합 toocreate 설정 하는 방법을 보여 줍니다. Azure 리소스 관리자 템플릿 만들기 및 Azure PowerShell을 사용 하 여 배포 하 여 크기 조정 설정 hello 눈금을 만들 있습니다. 템플릿에 대한 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하세요. 크기 집합의 자동 크기 조정에 대 한 더 toolearn 참조 [자동 크기 조정 및 가상 컴퓨터 크기 조정 설정](virtual-machine-scale-sets-autoscale-overview.md)합니다.

이 문서에서는 hello 다음 배포 리소스 및 확장:

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Insights.VMDiagnosticsSettings
* Microsoft.Insights/autoscaleSettings

Resource Manager 리소스에 대한 자세한 내용은 [Azure Resource Manager 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.

## <a name="step-1-install-azure-powershell"></a>1단계: Azure PowerShell 설치
참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello 최신 버전의 Azure PowerShell을 설치, 구독을 선택 하 고 tooAzure 로그인 하는 방법에 대 한 정보에 대 한 합니다.

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a>2단계: 리소스 그룹 및 저장소 계정 만들기
1. **리소스 그룹 만들기** – 모든 리소스는 배포 된 tooa 리소스 그룹 이어야 합니다. 사용 하 여 [새로 AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) 리소스 그룹 이름이 toocreate **vmsstestrg1**합니다.
2. **저장소 계정 만들기** –이 저장소 계정은 hello 템플릿이 보관 된입니다. 사용 하 여 [새로 AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) 라는 저장소 계정 toocreate **vmsstestsa**합니다.

## <a name="step-3-create-hello-template"></a>3 단계: hello 서식 파일 만들기
Azure 리소스 관리자 템플릿 toodeploy 있습니다 수 있도록 하 고 hello 리소스 및 관련된 배포 매개 변수의 JSON 설명을 사용 하 여 Azure 리소스를 함께 관리 합니다.

1. 선호 하는 편집기에서 hello 파일 C:\VMSSTemplate.json 만들고 hello 초기 JSON 구조 toosupport hello 템플릿을 추가 합니다.

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. 매개 변수는 항상 필수 이지만 제공 방법을 tooinput 값 hello 서식 파일이 배포 되는 경우. Toohello 템플릿을 추가한 hello 매개 변수 부모 요소 아래에 이러한 매개 변수를 추가 합니다.

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * Hello 눈금에 사용 되는 tooaccess hello 컴퓨터 있는 hello 별도 가상 컴퓨터에 대 한 이름이 설정 합니다.
    * hello 템플릿이 보관 된 hello 저장소 계정의 hello 이름입니다.
    * 가상 컴퓨터 tooinitially hello 수가 hello 크기 집합에 만듭니다.
    * hello 이름과 hello 가상 컴퓨터에 대 한 hello 관리자 계정의 암호입니다.
    * Toosupport hello 눈금 만들어진 hello 리소스에 대 한 이름 접두사를 설정 합니다.

3. 변수는 자주 변경 될 수 있는 템플릿 toospecify 값에 사용할 수 있습니다 또는 toobe 해야 하는 값이 매개 변수 값의 조합에서 생성 합니다. Toohello 템플릿을 추가한 hello 변수 부모 요소 아래에 이러한 변수를 추가 합니다.

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * Hello 네트워크 인터페이스에서 사용 되는 DNS 이름입니다.

        * hello IP 주소 이름 및 hello 가상 네트워크 및 서브넷에 대 한 접두사입니다.
        * hello 이름 및 식별자 hello 가상 네트워크의 부하 분산 장치, 및 네트워크 인터페이스.
        * Hello 크기 집합의 hello 컴퓨터와 연결 된 hello 계정에 대 한 저장소 계정 이름입니다.
        * Hello hello 가상 컴퓨터에 설치 된 진단 확장에 대 한 설정입니다. Hello 진단 확장에 대 한 자세한 내용은 참조 [모니터링 및 Azure 리소스 관리자 템플릿을 사용 하 여 진단을 사용 하 여 Windows 가상 컴퓨터를 만들](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

4. Hello 저장소 계정 리소스 toohello 템플릿을 추가한 hello 리소스 부모 요소 아래에 추가 합니다. 이 템플릿은 hello 운영 체제 디스크 및 진단 데이터 저장 된 다섯 개의 저장소 계정을 권장 루프 toocreate hello를 사용 합니다. 계정의이 집합 hello 현재 최대 크기 집합의 too100 가상 컴퓨터를 지원할 수 있습니다. 각 저장소 계정은 hello 서식 파일에 대 한 hello 매개 변수에서 제공 하는 hello 접두사와 함께 하는 hello 변수에 정의 된 문자 지정자도 지정 됩니다.

    ```json
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
      "apiVersion": "2015-06-15",
      "copy": {
        "name": "storageLoop",
        "count": 5
      },
      "location": "[resourceGroup().location]",
      "properties": { "accountType": "Standard_LRS" }
    },
    ```

5. Hello 가상 네트워크 리소스를 추가 합니다. 자세한 내용은 [네트워크 리소스 공급자](../virtual-network/resource-groups-networking.md)를 참조하세요.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. Hello 공용 IP 주소 리소스 hello에서 사용 되는 부하 분산 장치 및 네트워크 인터페이스를 추가 합니다.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. Hello 크기 집합에서 사용 되는 hello 부하 분산 장치 리소스를 추가 합니다. 자세한 내용은 [부하 분산 장치에 대한 Azure 리소스 관리자 지원](../load-balancer/load-balancer-arm.md)을 참조하세요.

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. Hello hello 별도 가상 컴퓨터에서 사용 되는 네트워크 인터페이스 리소스를 추가 합니다. 컴퓨터 크기 집합의 공용 IP 주소를 통해 액세스할 수 없습니다, 때문에 별도 가상 컴퓨터에에서 만들어집니다 hello 동일한 가상 네트워크 tooremotely 액세스 hello 컴퓨터.

    ```json  
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. Hello hello 크기 집합으로 동일한 네트워크에 hello 별도 가상 컴퓨터를 추가 합니다.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2012-R2-Datacenter",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
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
        }
      }
    },
    ```

10. Hello 가상 컴퓨터 크기 집합 리소스를 추가 하 고 hello 크기 집합의 모든 가상 컴퓨터에 설치 되어 있는 hello 진단 확장을 지정 합니다. 이 리소스에 대 한 hello 설정 중 대부분 hello 가상 컴퓨터 리소스와 비슷합니다. hello 주요 차이점은 hello 크기 집합의 가상 컴퓨터의 hello 수를 지정 하는 hello 용량 요소 및 upgradePolicy 업데이트 toovirtual 컴퓨터 적용 하는 방법을 지정 하는입니다. hello 크기 집합 만들어지지 모든 hello 저장소 계정이 생성 될 때까지 hello dependsOn 요소와 지정 된 대로 합니다.

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Hello 크기 집합 hello 크기 집합의 hello 머신에서 hello 프로세서 사용량에 따라 조정 방법을 정의 하는 hello autoscaleSettings 리소스를 추가 합니다.

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor(_Total)\\% Processor Time",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```

    이 자습서의 경우 다음 값이 중요합니다.
    
    * **metricName**  
    이 값은 hello wadperfcounter 변수에 정의한 hello 성능 카운터와 동일 hello 됩니다. 해당 변수를 사용 하 여 진단 확장 hello 수집 hello **Processor(_Total)\% 프로세서 시간** 카운터입니다.
    
    * **metricResourceUri**  
    이 값은 hello 가상 컴퓨터 크기 집합의 hello 리소스 식별자입니다.
    
    * **timeGrain**  
    이 값은 hello 메트릭을 수집 하는 hello 세분성입니다. 이 서식 파일에서 설정 tooone 분입니다.
    
    * **statistic**  
    이 값 hello 메트릭은 결합된 tooaccommodate hello 자동 작업 크기 조정 방법을 결정 합니다. hello 가능한 값은: 평균, 최소값, 최대값입니다. 이 서식 파일에서 hello 총 CPU 사용량의 hello 가상 컴퓨터를 수집 합니다.
    
    * **timeWindow**  
    이 값은 hello 인스턴스 데이터를 수집 하는 시간 범위입니다. 5분에서 12시간 사이여야 합니다.
    
    * **timeAggregation**  
    그의 값은 시간이 지남에 따라 수집 되는 hello 데이터를 결합 하는 방법을 결정 합니다. hello 기본값은 평균입니다. hello 가능한 값은: 평균, 최소값, 최대값, 마지막, 합계, 개수입니다.
    
    * **operator**  
    이 값은 hello 연산자가 사용 되는 toocompare hello 메트릭 데이터와 hello 임계값입니다. hello 가능한 값은: Equals, NotEquals, 보다 큼, GreaterThanOrEqual, LessThan, LessThanOrEqual 합니다.
    
    * **threshold**  
    이 값은 hello 크기 조정 작업을 트리거하는 hello 값입니다. 이 서식 파일에서 컴퓨터 toohello에 크기 집합 hello 평균 CPU 사용량이 hello 집합의 컴퓨터에 50% 초과 하는 경우 추가 됩니다.
    
    * **direction**  
    이 값은 hello 임계값이 작업을 수행 하는 경우 수행 하는 hello 동작을 결정 합니다. hello 가능한 값은 증가 또는 감소 합니다. 이 서식 파일에서 hello hello 크기 집합의 가상 컴퓨터 수가 증가 hello 임계값 hello 정의 된 기간에 50% 이상인 경우.
    
    * **type**  
    이 값은 hello 유형의 동작을 발생 해야 하며 tooChangeCount 설정 해야 합니다.
    
    * **값**  
    이 값은 추가 되거나 hello 크기 집합에서 제거 된 가상 컴퓨터의 hello 수입니다. 이 값은 1 이상이어야 합니다. hello 기본값은 1입니다. 이 서식 파일에서 hello 규모에 맞게 컴퓨터 hello 수 hello 임계값이 충족 하는 경우 1 씩 증가 설정 합니다.
    
    * **cooldown**  
    이 값은 hello 시간 toowait hello 마지막 크기 조정 작업 이후 hello 다음 작업이 발생 하기 전에. 이 값은 1분에서 1주 사이여야 합니다.

12. Hello 서식 파일을 저장 합니다.    

## <a name="step-4-upload-hello-template-toostorage"></a>4 단계: hello 템플릿 toostorage 업로드
hello 이름과 1 단계에서 만든 hello 저장소 계정의 기본 키를 알고으로 hello 서식 파일을 업로드할 수 있습니다.

1. Hello Microsoft Azure PowerShell 창에서 1 단계에서 만든 hello 저장소 계정의 hello 이름을 지정 하는 변수를 설정 합니다.
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. Hello hello 저장소 계정의 기본 키를 지정 하는 변수를 설정 합니다.
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   저장소 계정 리소스 hello hello Azure 포털에서에서 볼 때 hello 열쇠 아이콘을 클릭 하 여이 키를 얻을 수 있습니다.
3. hello 스토리지 계정으로 사용 되는 toovalidate 작업 하는 hello 저장소 계정 컨텍스트 개체를 만듭니다.
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. Hello 서식 파일을 저장 하기 위한 hello 컨테이너를 만듭니다.

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. Hello toohello 새 컨테이너 템플릿 파일을 업로드 합니다.

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a>5 단계: 배포 hello 서식 파일
Hello 서식 파일을 만든 했으므로 hello 리소스 배포를 시작할 수 있습니다. 이 명령은 toostart hello 프로세스를 사용 합니다.

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

키를 누르면 입력을 hello 변수 할당에 대 한 증명된 tooprovide 값 됩니다. 다음 값을 제공합니다.

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

모든 hello 리소스 toosuccessfully 배포에 대 일 분 정도 취해야 합니다.

> [!NOTE]
> Hello 포털의 기능 toodeploy hello 리소스를 사용할 수도 있습니다. 다음 링크를 사용합니다. "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"
> 
> 

## <a name="step-6-monitor-resources"></a>6단계: 리소스 모니터링
이러한 메서드를 사용하여 가상 컴퓨터 규모 집합에 대한 정보를 얻을 수 있습니다.

* Azure 포털 hello-현재 제한 된 양의 hello 포털을 사용 하 여 정보를 얻을 수 있습니다.
* hello [Azure 리소스 탐색기](https://resources.azure.com/) -이 도구는 hello hello 크기 집합의 현재 상태를 탐색에 가장 적합 합니다. 이 경로 따라 하 고 hello 눈금의 hello 인스턴스 보기 설정 하 여 만든 표시 되어야 합니다.
  
    구독 > {사용자의 구독} > resourceGroups > vmsstestrg1 > 공급자 > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines

* Azure PowerShell-이 명령은 tooget 일부 정보를 사용 합니다.

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  또는
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* Hello 눈금 집합 toomonitor 개별 프로세스에 hello 가상 컴퓨터에 원격으로 액세스할 수 있습니다 및 다른 컴퓨터는 것 처럼 toohello 별도 가상 컴퓨터를 연결 합니다.

> [!NOTE]
> 규모 집합에 대한 정보를 얻기 위해 전체 REST API를 [가상 컴퓨터 규모 집합](https://msdn.microsoft.com/library/mt589023.aspx)

## <a name="step-7-remove-hello-resources"></a>7 단계: hello 리소스를 제거 합니다.
Azure에서 사용 되는 리소스에 대 한 요금이 청구 되므로 항상 것은 더 이상 필요 없는 것이 좋습니다 toodelete 리소스입니다. 각 리소스는 리소스 그룹에서 별도로 toodelete을 필요 하지 않습니다. Hello 리소스 그룹을 삭제할 수 있습니다 및 모든 리소스를 자동으로 삭제 됩니다.

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

리소스 그룹 tookeep을 원하는 경우 hello에 크기 집합만 삭제할 수 있습니다.

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a>다음 단계
* 관리 방금 hello 크기 집합의 hello 정보를 사용 하 여 만든 [가상 컴퓨터 크기 집합의 가상 컴퓨터를 관리](virtual-machine-scale-sets-windows-manage.md)합니다.
* [가상 컴퓨터 확장 집합을 사용하여 수직 자동 크기 조정](virtual-machine-scale-sets-vertical-scale-reprovision.md)
* [Azure Monitor PowerShell 빠른 시작 샘플](../monitoring-and-diagnostics/insights-powershell-samples.md)에서 Azure Monitor 모니터링 기능 예제를 찾아보세요.
* 알림 기능에 대 한 자세한 내용은 [Azure 모니터에서 자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림 사용](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* 너무 방법에 대해 알아봅니다[Azure 모니터에서 사용 하 여 감사 로그를 toosend webhook 및 전자 메일 경고 알림](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

