---
title: "Windows VM 확장에 대 한 aaaSample 구성 | Microsoft Docs"
description: "확장으로 템플릿 작성에 대한 샘플 구성"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a1cee6c-51ea-4c03-b607-f158586d7175
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 7697be969dbcf609423f64b75c7edf80ca1bfd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-windows-vm-extension-configuration-samples"></a><span data-ttu-id="c19d0-103">Azure Windows VM 확장 구성 샘플</span><span class="sxs-lookup"><span data-stu-id="c19d0-103">Azure Windows VM Extension Configuration Samples</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c19d0-104">PowerShell - 템플릿</span><span class="sxs-lookup"><span data-stu-id="c19d0-104">PowerShell - Template</span></span>](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> * [<span data-ttu-id="c19d0-105">CLI - 템플릿</span><span class="sxs-lookup"><span data-stu-id="c19d0-105">CLI - Template</span></span>](../linux/extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="c19d0-106">이 문서에서는 Windows VM에 대해 Azure VM 확장을 구성하기 위한 샘플 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-106">This article provides sample configuration for configuring Azure VM Extensions for Windows VMs.</span></span>

<span data-ttu-id="c19d0-107">이러한 확장에 대해 자세히 toolearn 참조 [Azure VM 확장 개요입니다.](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c19d0-107">toolearn more about these extensions, see [Azure VM Extensions Overview.](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="c19d0-108">확장 템플릿 작성에 대해 자세히 toolearn 참조 [확장 템플릿을 작성 합니다.](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c19d0-108">toolearn more about authoring extension templates, see [Authoring Extension Templates.](extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="c19d0-109">이 문서는 hello Windows 확장 중 일부에 대해 예상 되는 구성 값을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-109">This article lists expected configuration values for some of hello Windows Extensions.</span></span>

## <a name="sample-template-snippet-for-vm-extensions-with-iaas-vms"></a><span data-ttu-id="c19d0-110">IaaS VM에서 VM 확장에 대한 샘플 템플릿 코드 조각</span><span class="sxs-lookup"><span data-stu-id="c19d0-110">Sample template snippet for VM Extensions with IaaS VMs.</span></span>
<span data-ttu-id="c19d0-111">다음과 같이 확장 검색 배포 하기 위한 템플릿 코드 조각 hello:</span><span class="sxs-lookup"><span data-stu-id="c19d0-111">hello template snippet for Deploying extensions looks as following:</span></span>

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

## <a name="sample-template-snippet-for-vm-extensions-with-vm-scale-sets"></a><span data-ttu-id="c19d0-112">VM 규모 집합에서 VM 확장에 대한 샘플 템플릿 코드 조각</span><span class="sxs-lookup"><span data-stu-id="c19d0-112">Sample template snippet for VM Extensions with VM Scale Sets.</span></span>
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

<span data-ttu-id="c19d0-113">Hello 확장을 배포 하기 전에 hello 최신 확장 버전을 확인 하 고 typeHandlerVersion"hello" hello 현재 최신 버전으로 교체 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c19d0-113">Before deploying hello extension please check hello latest extension version and replace hello "typeHandlerVersion" with hello current latest version.</span></span>

<span data-ttu-id="c19d0-114">Hello 문서의 나머지 부분에는 Windows VM 확장에 대 한 샘플 구성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-114">Rest of hello article provides sample configurations for Windows VM Extensions.</span></span>

<span data-ttu-id="c19d0-115">Hello 확장을 배포 하기 전에 hello 최신 확장 버전을 확인 하 고 typeHandlerVersion"hello" hello 현재 최신 버전으로 교체 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c19d0-115">Before deploying hello extension please check hello latest extension version and replace hello "typeHandlerVersion" with hello current latest version.</span></span>

### <a name="customscript-extension-14"></a><span data-ttu-id="c19d0-116">CustomScript 확장 1.4</span><span class="sxs-lookup"><span data-stu-id="c19d0-116">CustomScript Extension 1.4.</span></span>
      {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.4",
          "settings": {
              "fileUris": [
                  "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
              ],
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
          },
          "protectedSettings": {
            "storageAccountName": "yourStorageAccountName",
            "storageAccountKey": "yourStorageAccountKey"
          }
      }

#### <a name="parameter-description"></a><span data-ttu-id="c19d0-117">매개 변수 설명:</span><span class="sxs-lookup"><span data-stu-id="c19d0-117">Parameter description:</span></span>
* <span data-ttu-id="c19d0-118">fileUris: 쉼표로 구분 된 목록으로 hello 확장 하 여 hello VM에서 다운로드 하는 hello 파일의 url입니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-118">fileUris : Comma seperated list of urls of hello files that will be downloaded on hello VM by hello Extension.</span></span> <span data-ttu-id="c19d0-119">아무것도 지정하지 않으면 파일이 다운로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-119">No files are downloaded if nothing is specified.</span></span> <span data-ttu-id="c19d0-120">Hello 파일이 Azure 저장소에 경우 hello fileURLs를 전용으로 표시 될 수 있습니다 및 hello 해당 storageAccountName storageAccountKey 전달 될 수 및 개인 매개 변수가 tooaccess로 이러한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-120">If hello files are in Azure Storage, hello fileURLs can be marked private and hello correspoding storageAccountName and storageAccountKey can be passed as private parameters tooaccess these files.</span></span>
* <span data-ttu-id="c19d0-121">commandToExecute: [필수 매개 변수]: hello 확장으로 실행 되는 hello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-121">commandToExecute : [Mandatory Parameter] : This is hello command that will be executed by hello Extension.</span></span>
* <span data-ttu-id="c19d0-122">storageAccountName: [선택적 매개 변수]: 전용으로 표시 된 경우 hello fileURLs에 액세스 하기 위한 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-122">storageAccountName : [Optional Parameter] : Storage Account Name for accessing hello fileURLs, if they are marked as private.</span></span>
* <span data-ttu-id="c19d0-123">storageAccountKey: [선택적 매개 변수]: 전용으로 표시 된 경우 hello fileURLs에 액세스 하기 위한 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-123">storageAccountKey : [Optional Parameter] : Storage Account Key for accessing hello fileURLs, if they are marked as private.</span></span>

### <a name="customscript-extension-17"></a><span data-ttu-id="c19d0-124">CustomScript 확장 1.7</span><span class="sxs-lookup"><span data-stu-id="c19d0-124">CustomScript Extension 1.7.</span></span>
<span data-ttu-id="c19d0-125">매개 변수 설명에 대 한 tooCustomScript 버전 1.4를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c19d0-125">Please refer tooCustomScript version 1.4 for parameter description.</span></span> <span data-ttu-id="c19d0-126">버전 1.7에서는 스크립트 매개 변수(commandToExecute)를 protectedSettings로 보내는 작업을 지원하며 이 경우 매개 변수는 보내기 전에 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-126">Version 1.7 introduces support for sending script parameters(commandToExecute) as protectedSettings, in which case they will be encrypted before sending.</span></span> <span data-ttu-id="c19d0-127">'commandToExecute' 매개 변수는 settings 또는 protectedSettings 중 하나에만 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-127">'commandToExecute' parameter can be specified either in settings or protectedSettings but not in both.</span></span>

        {
            "publisher": "Microsoft.Compute",
            "type": "CustomScriptExtension",
            "typeHandlerVersion": "1.7",
            "settings": {
                "fileUris": [
                    "http: //Yourstorageaccount.blob.core.windows.net/customscriptfiles/start.ps1"
                ],
                "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1"
            },
            "protectedSettings": {
              "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -start.ps1",
              "storageAccountName": "yourStorageAccountName",
              "storageAccountKey": "yourStorageAccountKey"
            }
        }

### <a name="vmaccess-extension"></a><span data-ttu-id="c19d0-128">VMAccess 확장</span><span class="sxs-lookup"><span data-stu-id="c19d0-128">VMAccess Extension.</span></span>
      {
          "publisher": "Microsoft.Compute",
          "type": "VMAccessAgent",
          "typeHandlerVersion": "2.0",
          "settings": {
            "UserName" : "New User Name"
          },
          "protectedSettings": {
            "Password" : "New Password"
          }
      }

### <a name="dsc-extension"></a><span data-ttu-id="c19d0-129">DSC 확장</span><span class="sxs-lookup"><span data-stu-id="c19d0-129">DSC Extension.</span></span>
      {
          "publisher": "Microsoft.Powershell",
          "type": "DSC",
          "typeHandlerVersion": "2.1(Recommendation is toouse hello latest version)",
          "settings": {
              "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
              "SasToken": "Optional : SAS Token if ModulesUrl points tooAzure Blob Storage",
              "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
              "Properties": {
                  "ParameterToConfigurationFunction1": "Value1",
                  "ParameterToConfigurationFunction2": "Value2",
                  "ParameterOfTypePSCredential1": {
                      "UserName": "UsernameValue1",
                      "Password": "PrivateSettingsRef:Key1(Value is a reference tooa member of hello Items object in hello protected settings)"
                  },
                  "ParameterOfTypePSCredential2": {
                      "UserName": "UsernameValue2",
                      "Password": "PrivateSettingsRef:Key2"
                  }
              }
          },
          "protectedSettings": {
              "Items": {
                  "Key1": "PasswordValue1",
                  "Key2": "PasswordValue2"
              },
              "DataBlobUri": "optional : https: //UrlToConfigurationData.psd1"
          }
      }


### <a name="symantec-endpoint-protection"></a><span data-ttu-id="c19d0-130">Symantec Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="c19d0-130">Symantec Endpoint Protection.</span></span>
      {
        "publisher": "SymantecEndpointProtection",
        "type": "Symantec",
        "typeHandlerVersion": "12.1",
        "settings": {}
      }

### <a name="trend-micro-deep-security-agent"></a><span data-ttu-id="c19d0-131">Trend Micro Deep Security Agent</span><span class="sxs-lookup"><span data-stu-id="c19d0-131">Trend Micro Deep Security Agent.</span></span>
      {
        "publisher": "TrendMicro.DeepSecurity",
        "type": "TrendMicroDSA",
        "typeHandlerVersion": "9.6",
        "settings": {
          "ManagerAddress" : "Enter hello externally accessible DNS name or IP address of hello Deep Security Manager. Please enter \"agents.deepsecurity.trendmicro.com\" if using Deep Security as a Service",

          "ActivationPort" : "Enter hello port number of hello Deep Security Manager, default value - 443",

          "TenantIdentifier" : "Enter hello tenant ID, which is a hyphenated, 36-character string available in hello Deployment Scripts dialog box in hello Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "TenantActivationPassword" : "Enter hello tenant activation password, which is a hyphenated, 36-character string available in hello Deployment Scripts dialog box in hello Deep Security console. This parameter is mandatory if using Deep Security as a Service, or a multi-tenant installation of Deep Security Manager. Type NA if using a non multi-tenant installation of Deep Security Manager.",

          "SecurityPolicy" : "Optional : Enter hello name or numeric ID of hello security policy defined in hello Deep Security Manager which will be applied on agent activation tooprotect this virtual machine (recommended). No security policy will be applied toohello virtual machine if this parameter is blank. This parameter is optional if using Deep Security as a Service."
        }
      }

### <a name="vormertric-transparent-encryption-agent"></a><span data-ttu-id="c19d0-132">Vormertric Transparent Encryption Agent</span><span class="sxs-lookup"><span data-stu-id="c19d0-132">Vormertric Transparent Encryption Agent.</span></span>
            {
              "publisher": "Vormetric",
              "type": "VormetricTransparentEncryptionAgent",
              "typeHandlerVersion": "5.2",
              "settings": {
              }
            }

### <a name="puppet-enterprise-agent"></a><span data-ttu-id="c19d0-133">Puppet Enterprise Agent</span><span class="sxs-lookup"><span data-stu-id="c19d0-133">Puppet Enterprise Agent.</span></span>
            {
              "publisher": "PuppetLabs",
              "type": "PuppetEnterpriseAgent",
              "typeHandlerVersion": "3.2",
              "settings": {
                "puppet_master_server" : "Puppet Master Server Name"
              }
            }  

### <a name="microsoft-monitoring-agent-for-azure-operational-insights"></a><span data-ttu-id="c19d0-134">Microsoft Monitoring Agent for Azure Operational Insights</span><span class="sxs-lookup"><span data-stu-id="c19d0-134">Microsoft Monitoring Agent for Azure Operational Insights</span></span>
            {
              "publisher": "Microsoft.EnterpriseCloud.Monitoring",
              "type": "MicrosoftMonitoringAgent",
              "typeHandlerVersion": "1.0",
              "settings": {
                "workspaceId" : "hello Workspace ID is available from within hello Direct Agent Configuration section of hello Azure Operational Insights portal"
              }
              "protectedSettings": {
                "workspaceKey"  : "hello Workspace Key is a string that is available from within hello Direct Agent Configuration section of hello Azure Operational Insights portal"
              }
              }
            }

### <a name="mcafee-endpointsecurity"></a><span data-ttu-id="c19d0-135">McAfee EndpointSecurity</span><span class="sxs-lookup"><span data-stu-id="c19d0-135">McAfee EndpointSecurity</span></span>
            {
              "publisher": "McAfee.EndpointSecurity",
              "type": "McAfeeEndpointSecurity",
              "typeHandlerVersion": "6.0",
              "settings": {
                "entitlementKey" : "Optional : Enter a valid entitlement key or leave blank for trial version",
                "featureVS"      : "Choose whether or not tooinstall hello Virus and Spyware Protection features : true|false",
                "featureBP"      : "Choose whether or not tooinstall hello Browser Protection feature : true|false",
                "featureFW"      : "Choose whether or not tooinstall hello Firewall Protection feature :true|false",
                "relayServer"    : "Allows VMs on hello local subnet tooreceive updates through this VM when they are not connected toohello internet : true|false"
              }
            }

### <a name="azure-iaas-antimalware"></a><span data-ttu-id="c19d0-136">Azure IaaS Antimalware</span><span class="sxs-lookup"><span data-stu-id="c19d0-136">Azure IaaS Antimalware</span></span>
          {
            "publisher": "Microsoft.Azure.Security",
            "type": "IaaSAntimalware",
            "typeHandlerVersion": "1.2",
            "settings": {
              "AntimalwareEnabled": "true",
              "ExclusionsPaths"        : "Optional : ExclusionsPaths",
              "ExclusionsExtensions"   : "Optional : ExclusionsExtensions",
              "ExclusionsProcesses"   : "Optional : ExclusionsProcesses",
              "RealtimeProtectionEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsIsEnabled"   : "Optional : True|False",
              "ScheduledScanSettingsScanType"   : "Optional : Quick|Full",
              "ScheduledScanSettingsDay"   : "Optional : Sunday-Saturday",
              "ScheduledScanSettingsTime"   : "Optional : When tooperform hello scheduled scan, measured in minutes from midnight,0-1440"
            }
          }

### <a name="eset-file-security"></a><span data-ttu-id="c19d0-137">ESET File Security</span><span class="sxs-lookup"><span data-stu-id="c19d0-137">ESET File Security</span></span>
          {
            "publisher": "ESET",
            "type": "FileSecurity",
            "typeHandlerVersion": "6.0",
            "settings": {
            }
          }

### <a name="datadog-agent"></a><span data-ttu-id="c19d0-138">Datadog Agent</span><span class="sxs-lookup"><span data-stu-id="c19d0-138">Datadog Agent</span></span>
          {
            "publisher": "Datadog.Agent",
            "type": "DatadogWindowsAgent",
            "typeHandlerVersion": "0.5",
            "settings": {
              "api_key" : "API Key from https://app.datadoghq.com/account/settings#api"
            }
          }

### <a name="confer-advanced-threat-prevention-and-incident-response-for-azure"></a><span data-ttu-id="c19d0-139">Confer Advanced Threat Prevention and Incident Response for Azure</span><span class="sxs-lookup"><span data-stu-id="c19d0-139">Confer Advanced Threat Prevention and Incident Response for Azure</span></span>
          {
            "publisher": "Confer",
            "type": "ConferForAzure",
            "typeHandlerVersion": "1.0",
            "settings": {
              "ConferRegisterCode" : "Optional : Valid product registration code or leave it blank tooregister later",
              "ConferRegisterCode" : "Enter a valid server name if your account requires a dedicated confer backend server or leave it blank"
            }
          }

### <a name="cloudlink-securevm-agent"></a><span data-ttu-id="c19d0-140">CloudLink SecureVM Agent</span><span class="sxs-lookup"><span data-stu-id="c19d0-140">CloudLink SecureVM Agent</span></span>
          {
            "publisher": "CloudLinkEMC.SecureVM",
            "type": "CloudLinkSecureVMWindowsAgent",
            "typeHandlerVersion": "4.0",
            "settings": {
              "CloudLinkCenter" : "specify valid IP/FQDN tooCloudLinkCenter"
            }
          }

### <a name="barracuda-vpn-connectivity-agent-for-microsoft-azure"></a><span data-ttu-id="c19d0-141">Barracuda VPN Connectivity Agent for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c19d0-141">Barracuda VPN Connectivity Agent for Microsoft Azure</span></span>
          {
            "publisher": "Barracuda.Azure.ConnectivityAgent",
            "type": "BarracudaConnectivityAgent",
            "typeHandlerVersion": "3.5",
            "settings": {
              "ServerAddress" : "Host name or IP address of hello VPN server - AES, AES256, Blowfish,CAST,DES,3DES,None",
              "EncryptionAlgorithm" : "Algorithm used tooencrypt VPN traffic - MD5,SHA1,SHA256,None",
              "PKCS12File" : "Url for file containing certificate and private key used tooauthenticate against hello VPN server",
              "PKCS12FilePassword" : "Password for hello file containing certificate and private key"
            }
          }

### <a name="alert-logic-log-manager"></a><span data-ttu-id="c19d0-142">Alert Logic Log Manager</span><span class="sxs-lookup"><span data-stu-id="c19d0-142">Alert Logic Log Manager</span></span>
          {
            "publisher": "AlertLogic.Extension",
            "type": "AlertLogicLM",
            "typeHandlerVersion": "1.9",
            "settings": {
              "registrationKey" : " Alert Logic Log Manager registration key"
            }
          }

### <a name="chef-agent"></a><span data-ttu-id="c19d0-143">Chef Agent</span><span class="sxs-lookup"><span data-stu-id="c19d0-143">Chef Agent</span></span>
          {
            "publisher": "Chef.Bootstrap.WindowsAzure",
            "type": "ChefClient",
            "typeHandlerVersion": "1210.12",
            "settings": {
              "validation_key" : " Validation key",
              "client_rb" : "client_rb file",
              "runlist" : "Optional runlist"
            }
          }

### <a name="azure-diagnostics"></a><span data-ttu-id="c19d0-144">Azure 진단</span><span class="sxs-lookup"><span data-stu-id="c19d0-144">Azure Diagnostics</span></span>
<span data-ttu-id="c19d0-145">방법에 대 한 자세한 내용은 tooconfigure 진단 참조 [Azure 진단 확장](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c19d0-145">For more details about how tooconfigure diagnostics, see [Azure Diagnostics Extension](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

          {
            "publisher": "Microsoft.Azure.Diagnostics",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "1.5",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "xmlCfg": "[base64(variables('wadcfgx'))]",
              "storageAccount": "[parameters('diagnosticsStorageAccount')]"
            },
            "protectedSettings": {
            "storageAccountName": "[parameters('diagnosticsStorageAccount')]",
            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
            "storageAccountEndPoint": "https://core.windows.net"
          }
          }

### <a name="octopus-deploy-tentacle-agent"></a><span data-ttu-id="c19d0-146">Octopus Deploy Tentacle 에이전트</span><span class="sxs-lookup"><span data-stu-id="c19d0-146">Octopus Deploy Tentacle Agent</span></span>

<span data-ttu-id="c19d0-147">Tooconfigure Azure에서 여러 분기 배포 Tentacle hello 하는 방법에 대 한 자세한 내용은 참조 hello [여러 분기 설명서](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines)합니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-147">For more details about how tooconfigure hello Octopus Deploy Tentacle on Azure, see hello [Octopus Documentation](https://octopus.com/docs/installation/installing-tentacles/azure-virtual-machines).</span></span>

          {
            "publisher": "OctopusDeploy.Tentacle",
            "type": "OctopusDeployWindowsTentacle",
            "typeHandlerVersion": "2.0",
            "autoUpgradeMinorVersion": "true",
            "settings": {
              "OctopusServerUrl": "(string, required) hello url toohello Octopus server portal.",
              "Environments": [ "(array of strings, required) hello environments toowhich hello Tentacle should be added." ],
              "Roles": [ "(array of strings, required) hello roles tooassign toohello Tentacle." ],
              "CommunicationMode": "(string, required) Whether hello Tentacle should wait for connections from hello server ('Listen') or should poll hello server ('Poll').",
              "Port": (int, required) hello port toolisten on for connections from hello server (in 'Listen' mode), or hello port on which tooconnect toohello Octopus server ('Poll' mode).,
              "PublicHostNameConfiguration": "(string, optional) If in listening mode, how hello server should contact hello Tentacle. Can be 'PublicIP', 'FQDN', 'ComputerName' or 'Custom'. Defaults too'PublicIp'.",
              "CustomPublicHostName": "(string, optional) If in listening mode, and 'PublicHostNameConfiguration' is set too'Custom', hello address that hello server should use for this Tentacle.",
              "MachinePolicy": "(string, optional) hello Machine Policy tooassign toohello Tentacle. If not specified, uses hello default Machine Policy.",
              "Tenants": [ "(array of strings, optional) hello tenants tooassign toohello Tentacle. hello tenants feature must be enabled on hello Octopus Server." ],
              "TenantTags": [ "(array of strings, optional) hello tenant tags tooassign toohello Tentacle, in hello format 'TagSet/TagName'. hello tenants feature must be enabled on hello Octopus Server." ]
            },
            "protectedSettings": {
              "ApiKey": "(string, required) hello Api Key toouse tooconnect toohello Octopus server."
            }
          }

<span data-ttu-id="c19d0-148">위의 hello 예에 hello 버전 번호 hello 최신 버전 번호로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-148">In hello examples above, replace hello version number with hello latest version number.</span></span>

<span data-ttu-id="c19d0-149">다음은 사용자 지정 스크립트 확장을 사용하는 전체 VM 템플릿의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c19d0-149">Here is an example of a full VM template with Custom Script Extension.</span></span>

[<span data-ttu-id="c19d0-150">Windows VM의 사용자 지정 스크립트 확장</span><span class="sxs-lookup"><span data-stu-id="c19d0-150">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

