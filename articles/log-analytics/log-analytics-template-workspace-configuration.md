---
title: "Azure 리소스 관리자 템플릿 tooCreate aaaUse 로그 분석 작업 영역 구성 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 toocreate를 사용 하 여 구성 하는 로그 분석 작업 영역입니다."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: d21ca1b0-847d-4716-bb30-2a8c02a606aa
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: json
ms.topic: article
ms.date: 06/01/2017
ms.author: richrund
ms.openlocfilehash: c8f413e982f5eeed73f463524ff6f239f26c9127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-azure-resource-manager-templates"></a><span data-ttu-id="b0aa0-103">Azure Resource Manager 템플릿 사용한 Log Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="b0aa0-103">Manage Log Analytics using Azure Resource Manager templates</span></span>
<span data-ttu-id="b0aa0-104">사용할 수 있습니다 [Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md) toocreate 및 로그 분석 작업 영역을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0aa0-104">You can use [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toocreate and configure Log Analytics workspaces.</span></span> <span data-ttu-id="b0aa0-105">템플릿 수행할 수 있는 hello 작업의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="b0aa0-105">Examples of hello tasks you can perform with templates include:</span></span>

* <span data-ttu-id="b0aa0-106">작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="b0aa0-106">Create a workspace</span></span>
* <span data-ttu-id="b0aa0-107">솔루션 추가</span><span class="sxs-lookup"><span data-stu-id="b0aa0-107">Add a solution</span></span>
* <span data-ttu-id="b0aa0-108">저장된 검색 만들기</span><span class="sxs-lookup"><span data-stu-id="b0aa0-108">Create saved searches</span></span>
* <span data-ttu-id="b0aa0-109">컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b0aa0-109">Create a computer group</span></span>
* <span data-ttu-id="b0aa0-110">Hello Windows 에이전트가 설치 된 컴퓨터에서 IIS 로그의 컬렉션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b0aa0-110">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="b0aa0-111">Linux 및 Windows 컴퓨터에서 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="b0aa0-111">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="b0aa0-112">Linux 컴퓨터의 syslog에서 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="b0aa0-112">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="b0aa0-113">Windows 이벤트 로그에서 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="b0aa0-113">Collect events from Windows event logs</span></span>
* <span data-ttu-id="b0aa0-114">사용자 지정 이벤트 로그 수집</span><span class="sxs-lookup"><span data-stu-id="b0aa0-114">Collect custom event logs</span></span>
* <span data-ttu-id="b0aa0-115">Hello 로그 분석 에이전트 tooan Azure 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0aa0-115">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="b0aa0-116">Azure 진단을 사용 하 여 수집 된 로그 분석 tooindex 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="b0aa0-116">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="b0aa0-117">이 문서는 템플릿을 템플릿에서 수행할 수 있는 hello 구성의 일부를 보여 주는 샘플을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0aa0-117">This article provides a template samples that illustrate some of hello configuration that you can perform from templates.</span></span>

## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="b0aa0-118">Log Analytics 작업 영역 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="b0aa0-118">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="b0aa0-119">hello 다음 서식 파일 예제에서는 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="b0aa0-119">hello following template sample illustrates how to:</span></span>

1. <span data-ttu-id="b0aa0-120">데이터 보존 설정을 포함하는 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="b0aa0-120">Create a workspace, including setting data retention</span></span>
2. <span data-ttu-id="b0aa0-121">추가 솔루션 toohello 작업 영역</span><span class="sxs-lookup"><span data-stu-id="b0aa0-121">Add solutions toohello workspace</span></span>
3. <span data-ttu-id="b0aa0-122">저장된 검색 만들기</span><span class="sxs-lookup"><span data-stu-id="b0aa0-122">Create saved searches</span></span>
4. <span data-ttu-id="b0aa0-123">컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b0aa0-123">Create a computer group</span></span>
5. <span data-ttu-id="b0aa0-124">Hello Windows 에이전트가 설치 된 컴퓨터에서 IIS 로그의 컬렉션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b0aa0-124">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
6. <span data-ttu-id="b0aa0-125">Linux 컴퓨터에서 논리 디스크 성능 카운터 수집(사용된 Inode 비율, 사용 가능한 MB, 사용된 공간 비율, 초당 디스크 전송, 초당 디스크 읽기, 초당 디스크 쓰기)</span><span class="sxs-lookup"><span data-stu-id="b0aa0-125">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
7. <span data-ttu-id="b0aa0-126">Linux 컴퓨터에서 syslog 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="b0aa0-126">Collect syslog events from Linux computers</span></span>
8. <span data-ttu-id="b0aa0-127">Windows 컴퓨터에서 hello 응용 프로그램 이벤트 로그에서에서 오류 및 경고 이벤트를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0aa0-127">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
9. <span data-ttu-id="b0aa0-128">Windows 컴퓨터에서 사용 가능한 메모리(MB) 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="b0aa0-128">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
10. <span data-ttu-id="b0aa0-129">사용자 지정 로그 수집</span><span class="sxs-lookup"><span data-stu-id="b0aa0-129">Collect a custom log</span></span> 
11. <span data-ttu-id="b0aa0-130">IIS 로그 및 Azure 진단 tooa 저장소 계정에 의해 작성 된 Windows 이벤트 로그 수집</span><span class="sxs-lookup"><span data-stu-id="b0aa0-130">Collect IIS logs and Windows Event logs written by Azure diagnostics tooa storage account</span></span>

```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "workspaceName": {
      "type": "string",
      "metadata": {
        "description": "workspaceName"
      }
    },
    "serviceTier": {
      "type": "string",
      "allowedValues": [
        "Free",
        "Standalone",
        "PerNode"
      ],
      "metadata": {
        "description": "Service Tier: Free, Standalone, or PerNode"
    }
      },
    "dataRetention": {
      "type": "int",
      "defaultValue": 30,
      "minValue": 7,
      "maxValue": 730,
      "metadata": {
        "description": "Number of days of retention. Free plans can only have 7 days, Standalone and OMS plans include 30 days for free"
      }
    },
    "location": {
      "type": "string",
      "allowedValues": [
        "East US",
        "West Europe",
        "Southeast Asia",
        "Australia Southeast"
      ]
    },
    "applicationDiagnosticsStorageAccountName": {
        "type": "string",
        "metadata": {
          "description": "Name of hello storage account with Azure diagnostics output"
        }
    },
    "applicationDiagnosticsStorageAccountResourceGroup": {
        "type": "string",
        "metadata": {
          "description": "hello resource group name containing hello storage account with Azure diagnostics output"
        }
    }
  },
  "variables": {
    "Updates": {
      "Name": "[Concat('Updates', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "Updates"
    },
    "AntiMalware": {
      "Name": "[concat('AntiMalware', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "AntiMalware"
    },
    "SQLAssessment": {
      "Name": "[Concat('SQLAssessment', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "SQLAssessment"
    },
    "diagnosticsStorageAccount": "[resourceId(parameters('applicationDiagnosticsStorageAccountResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName'))]"
  },
  "resources": [
    {
      "apiVersion": "2015-11-01-preview",
      "type": "Microsoft.OperationalInsights/workspaces",
      "name": "[parameters('workspaceName')]",
      "location": "[parameters('location')]",
      "properties": {
        "sku": {
          "Name": "[parameters('serviceTier')]"
        },
    "retention": "[parameters('dataRetention')]"
      },
      "resources": [
        {
          "apiVersion": "2015-11-01-preview",
          "name": "VMSS Queries2",
          "type": "savedSearches",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "Category": "VMSS",
            "ETag": "*",
            "DisplayName": "VMSS Instance Count",
            "Query": "Type:Event Source=ServiceFabricNodeBootstrapAgent | dedup Computer | measure count () by Computer",
            "Version": 1
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsEvent1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsEvent",
          "properties": {
            "eventLogName": "Application",
            "eventTypes": [
              {
                "eventType": "Error"
              },
              {
                "eventType": "Warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsPerfCounter1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsPerformanceCounter",
          "properties": {
            "objectName": "Memory",
            "instanceName": "*",
            "intervalSeconds": 10,
            "counterName": "Available MBytes"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleIISLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "IISLogs",
          "properties": {
            "state": "OnPremiseEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslog",
          "properties": {
            "syslogName": "kern",
            "syslogSeverities": [
              {
                "severity": "emerg"
              },
              {
                "severity": "alert"
              },
              {
                "severity": "crit"
              },
              {
                "severity": "err"
              },
              {
                "severity": "warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslogCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerf1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceObject",
          "properties": {
            "performanceCounters": [
              {
                "counterName": "% Used Inodes"
              },
              {
                "counterName": "Free Megabytes"
              },
              {
                "counterName": "% Used Space"
              },
              {
                "counterName": "Disk Transfers/sec"
              },
              {
                "counterName": "Disk Reads/sec"
              },
              {
                "counterName": "Disk Writes/sec"
              }
            ],
            "objectName": "Logical Disk",
            "instanceName": "*",
            "intervalSeconds": 10
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerfCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLog",
          "properties": {
            "customLogName": "sampleCustomLog1",
            "description": "test custom log datasources",
            "inputs": [
              {
                "location": {
                  "fileSystemLocations": {
                    "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ],
                    "linuxFileTypeLogPaths": [ "/var/logs" ]
                  }
                },
                "recordDelimiter": {
                  "regexDelimiter": {
                    "pattern": "\\n",
                    "matchIndex": 0,
                    "matchIndexSpecified": true,
                    "numberedGroup": null
                  }
                }
              }
            ],
            "extractions": [
              {
                "extractionName": "TimeGenerated",
                "extractionType": "DateTime",
                "extractionProperties": {
                  "dateTimeExtraction": {
                    "regex": null,
                    "joinStringRegex": null
                  }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLogCollection",
          "properties": {
            "state": "LinuxLogsEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "name": "[concat(parameters('applicationDiagnosticsStorageAccountName'),parameters('workspaceName'))]",
          "type": "storageinsightconfigs",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "containers": [ 
              "wad-iis-logfiles" 
            ],
            "tables": [
              "WADWindowsEventLogsTable"
            ],
            "storageAccount": {
              "id": "[variables('diagnosticsStorageAccount')]",
              "key": "[listKeys(variables('diagnosticsStorageAccount'),'2015-06-15').key1]"
            }
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('Updates').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('Updates').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('Updates').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('Updates').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('AntiMalware').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('AntiMalware').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('AntiMalware').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('AntiMalware').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('SQLAssessment').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('SQLAssessment').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('SQLAssessment').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('SQLAssessment').GalleryName)]",
            "promotionCode": ""
          }
        }
      ]
    }
  ],
  "outputs": {
    "workspaceOutput": {
      "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-11-01-preview')]",
      "type": "object"
    }
  }
}

```
### <a name="deploying-hello-sample-template"></a><span data-ttu-id="b0aa0-131">Hello 예제 서식 파일 배포</span><span class="sxs-lookup"><span data-stu-id="b0aa0-131">Deploying hello sample template</span></span>
<span data-ttu-id="b0aa0-132">toodeploy hello 샘플 템플릿:</span><span class="sxs-lookup"><span data-stu-id="b0aa0-132">toodeploy hello sample template:</span></span>

1. <span data-ttu-id="b0aa0-133">예를 들어 hello 연결 된 샘플을 파일로 저장`azuredeploy.json`</span><span class="sxs-lookup"><span data-stu-id="b0aa0-133">Save hello attached sample in a file, for example `azuredeploy.json`</span></span> 
2. <span data-ttu-id="b0aa0-134">원하는 hello 템플릿 toohave hello 구성 편집</span><span class="sxs-lookup"><span data-stu-id="b0aa0-134">Edit hello template toohave hello configuration you want</span></span>
3. <span data-ttu-id="b0aa0-135">PowerShell 또는 hello 명령줄 toodeploy hello 템플릿을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b0aa0-135">Use PowerShell or hello command line toodeploy hello template</span></span>

#### <a name="powershell"></a><span data-ttu-id="b0aa0-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0aa0-136">PowerShell</span></span>
`New-AzureRmResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile azuredeploy.json`

#### <a name="command-line"></a><span data-ttu-id="b0aa0-137">명령 줄</span><span class="sxs-lookup"><span data-stu-id="b0aa0-137">Command line</span></span>
```
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> --TemplateFile azuredeploy.json
```


## <a name="example-resource-manager-templates"></a><span data-ttu-id="b0aa0-138">Resource Manager 템플릿 예</span><span class="sxs-lookup"><span data-stu-id="b0aa0-138">Example Resource Manager templates</span></span>
<span data-ttu-id="b0aa0-139">로그 분석을 포함 하 여에 대 한 여러 템플릿을 포함 하는 hello Azure 빠른 시작 템플릿 갤러리:</span><span class="sxs-lookup"><span data-stu-id="b0aa0-139">hello Azure quickstart template gallery includes several templates for Log Analytics, including:</span></span>

* [<span data-ttu-id="b0aa0-140">로그 분석 VM 확장 hello로 Windows를 실행 하는 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="b0aa0-140">Deploy a virtual machine running Windows with hello Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-windows-vm/)
* [<span data-ttu-id="b0aa0-141">로그 분석 VM 확장 hello로 Linux를 실행 하는 가상 컴퓨터 배포</span><span class="sxs-lookup"><span data-stu-id="b0aa0-141">Deploy a virtual machine running Linux with hello Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-ubuntu-vm/)
* [<span data-ttu-id="b0aa0-142">기존 Log Analytics 작업 영역을 사용하여 Azure Site Recovery 모니터링</span><span class="sxs-lookup"><span data-stu-id="b0aa0-142">Monitor Azure Site Recovery using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/asr-oms-monitoring/)
* [<span data-ttu-id="b0aa0-143">기존 Log Analytics 작업 영역을 사용하여 Azure Web Apps 모니터링</span><span class="sxs-lookup"><span data-stu-id="b0aa0-143">Monitor Azure Web Apps using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-webappazure-oms-monitoring/)
* [<span data-ttu-id="b0aa0-144">기존 Log Analytics 작업 영역을 사용하여 SQL Azure 모니터링</span><span class="sxs-lookup"><span data-stu-id="b0aa0-144">Monitor SQL Azure using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-sqlazure-oms-monitoring/)
* [<span data-ttu-id="b0aa0-145">Service Fabric 클러스터 배포 및 기존 Log Analytics 작업 영역을 사용하여 모니터링</span><span class="sxs-lookup"><span data-stu-id="b0aa0-145">Deploy a Service Fabric cluster and monitor it with an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-oms/)
* [<span data-ttu-id="b0aa0-146">서비스 패브릭 클러스터를 배포 하 고 로그 분석 작업 영역 toomonitor 만들 것</span><span class="sxs-lookup"><span data-stu-id="b0aa0-146">Deploy a Service Fabric cluster and create a Log Analytics workspace toomonitor it</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-vmss-oms/)

## <a name="next-steps"></a><span data-ttu-id="b0aa0-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b0aa0-147">Next steps</span></span>
* [<span data-ttu-id="b0aa0-148">Resource Manager 템플릿을 사용하여 Azure VM에 에이전트 배포</span><span class="sxs-lookup"><span data-stu-id="b0aa0-148">Deploy agents into Azure VMs using Resource Manager templates</span></span>](log-analytics-azure-vm-extension.md)

