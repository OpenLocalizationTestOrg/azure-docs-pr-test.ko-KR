---
title: "Linux VM 확장에 대 한 aaaSample 구성 | Microsoft Docs"
description: "Linux VM용 확장을 사용하여 템플릿을 작성하기 위한 샘플 구성"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f50e6b2-fce0-41ef-823d-df433957601a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/13/2016
ms.author: kundanap
ms.openlocfilehash: bc19b8d7d6fdb1783be99ec7fdd5cde5e1f8ca80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="linux-vm-extension-configuration-samples"></a><span data-ttu-id="e046a-103">Linux VM 확장 구성 샘플</span><span class="sxs-lookup"><span data-stu-id="e046a-103">Linux VM extension configuration samples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e046a-104">PowerShell - 템플릿</span><span class="sxs-lookup"><span data-stu-id="e046a-104">PowerShell - Template</span></span>](../windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [<span data-ttu-id="e046a-105">CLI - 템플릿</span><span class="sxs-lookup"><span data-stu-id="e046a-105">CLI - Template</span></span>](../windows/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="e046a-106">이 문서에서는 Linux VM에 대해 Azure VM 확장을 구성하기 위한 샘플 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e046a-106">This article provides sample configuration for configuring Azure VM extensions for Linux VMs.</span></span>

<span data-ttu-id="e046a-107">이러한 확장에 대 한 자세한 여기를 클릭 하십시오 toolearn: [Azure VM 확장 개요입니다.](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e046a-107">toolearn more about these extensions click here : [Azure VM Extensions Overview.](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="e046a-108">여기를 클릭 하는 확장 템플릿을 작성 하는 방법에 대 한 내용은 toolearn: [확장 템플릿 제작 합니다.](../windows/extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e046a-108">toolearn more about authoring extension templates click here : [Authoring Extension Templates.](../windows/extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="e046a-109">이 문서는 Linux 확장 hello 중 일부에 대해 예상 되는 구성 값을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e046a-109">This article lists expected configuration values for some of hello Linux Extensions.</span></span>

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="e046a-110">VM 확장에 대한 샘플 템플릿 코드 조각</span><span class="sxs-lookup"><span data-stu-id="e046a-110">Sample template snippet for VM Extensions.</span></span>
<span data-ttu-id="e046a-111">다음과 같이 확장 검색 배포 하기 위한 템플릿 코드 조각 hello:</span><span class="sxs-lookup"><span data-stu-id="e046a-111">hello template snippet for Deploying extensions looks as following:</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "autoUpgradeMinorVersion":true,
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a><span data-ttu-id="e046a-112">VM 규모 집합에서 VM 확장에 대한 샘플 템플릿 코드 조각</span><span class="sxs-lookup"><span data-stu-id="e046a-112">Sample template snippet for VM Extensions with VM Scale Sets.</span></span>
          {
           "type":"Microsoft.Compute/virtualMachineScaleSets",
          ....
                 "extensionProfile":{
                 "extensions":[
                   {
                     "name":"extension Name",
                     "properties":{
                       "publisher":"Publisher Namespace",
                       "type":"extension Name",
                       "typeHandlerVersion":"extension version",
                       "autoUpgradeMinorVersion":true,
                       "settings":{
                       // Extension specific configuration goes in here.
                       }
                     }
                    }
                  }
                }

<span data-ttu-id="e046a-113">Hello 확장을 배포 하기 전에 hello 최신 확장 버전을 확인 하 고 typeHandlerVersion"hello" hello 현재 최신 버전으로 교체 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e046a-113">Before deploying hello extension please check hello latest extension version and replace hello "typeHandlerVersion" with hello current latest version.</span></span>

<span data-ttu-id="e046a-114">Hello 문서의 나머지 부분에는 Linux VM 확장에 대 한 샘플 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e046a-114">Rest of hello article provides sample configurations for Linux VM Extensions.</span></span>

### <a name="cloudlink-securevm-agent"></a><span data-ttu-id="e046a-115">CloudLink SecureVM Agent</span><span class="sxs-lookup"><span data-stu-id="e046a-115">CloudLink SecureVM Agent</span></span>
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMLinuxAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN tooCloudLinkCenter"
            }
          }

### <a name="customscript-extension-for-linux"></a><span data-ttu-id="e046a-116">Linux용 CustomScript 확장</span><span class="sxs-lookup"><span data-stu-id="e046a-116">CustomScript Extension for Linux.</span></span>
    {
        "publisher": " Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
            ],
            "commandToExecute": "powershell.exe-ExecutionPolicyUnrestricted-Filestart.ps1"
        }
    }


### <a name="datadog-agent"></a><span data-ttu-id="e046a-117">Datadog Agent</span><span class="sxs-lookup"><span data-stu-id="e046a-117">Datadog Agent</span></span>
        {
          "publisher": "Datadog.Agent",
          "type": "DatadogLinuxAgent",
          "typeHandlerVersion": "0.4",
          "settings": {
            "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
          }
        }

### <a name="chef-agent"></a><span data-ttu-id="e046a-118">Chef Agent</span><span class="sxs-lookup"><span data-stu-id="e046a-118">Chef Agent</span></span>
        {
          "publisher": "Chef.Bootstrap.WindowsAzure",
          "type": "CentosChefClient|LinuxChefClient",
          "typeHandlerVersion": "1210.12",
          "settings": {
            "validation_key" : " Validation key",
            "client_rb" : "client_rb file",
            "runlist" : "Optional runlist"
          }
        }

### <a name="vm-access-extension-password-reset"></a><span data-ttu-id="e046a-119">VM Access 확장(암호 재설정)</span><span class="sxs-lookup"><span data-stu-id="e046a-119">VM Access Extension (Password Reset)</span></span>
<span data-ttu-id="e046a-120">업데이트 된 스키마에 대 한 참조 toohello [VMAccessForLinux 설명서](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)</span><span class="sxs-lookup"><span data-stu-id="e046a-120">For updated schema refer toohello [VMAccessForLinux Documentation](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)</span></span>

        {
          "publisher": "Microsoft.OSTCExtensions",
          "type": "VMAccessForLinux",
          "typeHandlerVersion": "1.2",
          "protectedSettings": {
            "username": "(required, string) hello name of hello user",
            "password": "(optional, string) hello password of hello user",
            "reset_ssh": "(optional, boolean) whether or not reset hello ssh",
            "ssh_key": "(optional, string) hello public key of hello user, base64 encoded pem",
            "remove_user": "(optional, string) hello user name tooremove"
          }
        }

### <a name="os-patching"></a><span data-ttu-id="e046a-121">OS 패치</span><span class="sxs-lookup"><span data-stu-id="e046a-121">OS Patching</span></span>
<span data-ttu-id="e046a-122">업데이트 된 스키마에 대 한 참조 toohello [OSPatching 설명서](https://github.com/Azure/azure-linux-extensions/tree/master/OSPatching)</span><span class="sxs-lookup"><span data-stu-id="e046a-122">For updated schema refer toohello [OSPatching Documentation](https://github.com/Azure/azure-linux-extensions/tree/master/OSPatching)</span></span>

        {
        "publisher": "Microsoft.OSTCExtensions",
        "type": "OSPatchingForLinux",
        "typeHandlerVersion": "2.9",
        "Settings": {
          "disabled": false,
          "stop": false,
          "rebootAfterPatch": "RebootIfNeed|Required|NotRequired|Auto",
          "category": "Important|ImportantAndRecommended",
          "installDuration": "<hr:min>",
          "oneoff": false,
          "intervalOfWeeks": "<number>",
          "dayOfWeek": "Sunday|Monday|Tuesday|Wednesday|Thursday|Friday|Saturday|Everyday",
          "startTime": "<hr:min>",
          "vmStatusTest": {
              "local": false,
              "idleTestScript": "<path_to_idletestscript>",
              "healthyTestScript": "<path_to_healthytestscript>"
          }
        }
        }

### <a name="docker-extension"></a><span data-ttu-id="e046a-123">Docker 확장</span><span class="sxs-lookup"><span data-stu-id="e046a-123">Docker Extension</span></span>
<span data-ttu-id="e046a-124">업데이트 된 스키마에 대 한 참조 toohello [Docker 확장 문서](https://github.com/Azure/azure-docker-extension/blob/master/README.md#1-configuration-schema)</span><span class="sxs-lookup"><span data-stu-id="e046a-124">For updated schema refer toohello [Docker Extension Documentation](https://github.com/Azure/azure-docker-extension/blob/master/README.md#1-configuration-schema)</span></span>

        {
          "publisher": "Microsoft.Azure.Extensions ",
          "type": "DockerExtension ",
          "typeHandlerVersion": "1.0",
          "Settings": {
            "docker":{
                "port": "2376",
                "options": ["-D", "--dns=8.8.8.8"]
            },
            "compose": {
                "cache" : {
                    "image" : "memcached",
                    "ports" : ["11211:11211"]
                },
                "blog": {
                    "image": "ghost",
                    "ports": ["80:2368"]
                }
            }
            }
        }

        ### Linux Diagnostics Extension
        {
        "storageAccountName": "storage account tooreceive data",
        "storageAccountKey": "key of hello account",
        "perfCfg": [
        {
            "query": "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
            "table": "LinuxMemory"
        }
        ],
        "fileCfg": [
        {
            "file": "/var/log/mysql.err",
            "table": "mysqlerr"
        }
        ]
        }

<span data-ttu-id="e046a-125">위의 hello 예에 hello 버전 번호 hello 최신 버전 번호로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e046a-125">In hello examples above, replace hello version number with hello latest version number.</span></span>

<span data-ttu-id="e046a-126">다음은 확장을 사용하여 Linux VM을 만들기 위한 전체 VM 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="e046a-126">Here is a full VM template for creating a Linux VM with an extension:</span></span>

[<span data-ttu-id="e046a-127">Linux VM의 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="e046a-127">Custom Script Extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

