---
title: "상태 구성 리소스 관리자 템플릿 aaaDesired | Microsoft Docs"
description: "Azure에서 원하는 상태 구성에 대한 Resource Manager 템플릿 정의 및 예제와 문제 해결"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="a5bb4-103">Azure Resource Manager 템플릿을 사용하여 Windows VMSS 및 원하는 상태 구성</span><span class="sxs-lookup"><span data-stu-id="a5bb4-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="a5bb4-104">이 문서에서는 hello에 대 한 hello 리소스 관리자 템플릿을 설명 [필요한 상태 구성 확장 처리기](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="a5bb4-105">Windows VM의 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="a5bb4-105">Template example for a Windows VM</span></span>
<span data-ttu-id="a5bb4-106">hello 다음 코드 조각은 들어갑니다 hello hello 템플릿의 리소스 섹션.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-106">hello following snippet goes into hello Resource section of hello template.</span></span>

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="a5bb4-107">Windows VMSS의 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="a5bb4-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="a5bb4-108">VMSS 노드 "VirtualMachineProfile" hello "extensionProfile" 특성으로 "속성" 섹션을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="a5bb4-109">"extensions" 아래에 DSC가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-109">DSC is added under "extensions".</span></span> 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a><span data-ttu-id="a5bb4-110">자세한 설정 정보</span><span class="sxs-lookup"><span data-stu-id="a5bb4-110">Detailed Settings Information</span></span>
<span data-ttu-id="a5bb4-111">hello 다음 스키마는 hello Azure Resource Manager 템플릿에 Azure DSC 확장의 hello 설정 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a><span data-ttu-id="a5bb4-112">세부 정보</span><span class="sxs-lookup"><span data-stu-id="a5bb4-112">Details</span></span>
| <span data-ttu-id="a5bb4-113">속성 이름</span><span class="sxs-lookup"><span data-stu-id="a5bb4-113">Property Name</span></span> | <span data-ttu-id="a5bb4-114">형식</span><span class="sxs-lookup"><span data-stu-id="a5bb4-114">Type</span></span> | <span data-ttu-id="a5bb4-115">설명</span><span class="sxs-lookup"><span data-stu-id="a5bb4-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a5bb4-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="a5bb4-116">settings.wmfVersion</span></span> |<span data-ttu-id="a5bb4-117">string</span><span class="sxs-lookup"><span data-stu-id="a5bb4-117">string</span></span> |<span data-ttu-id="a5bb4-118">Hello VM에 설치 되어야 하는 Windows 관리 프레임 워크의 hello 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="a5bb4-119">이 속성 too'latest 설정 ' wmf hello 가장 업데이트 된 버전 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="a5bb4-120">이 속성에 대 한 hello 현재 가능한 값은 **'4.0', '5.0', ' 5.0PP' 및 'latest'**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="a5bb4-121">이러한 가능한 값은 주체 tooupdates 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="a5bb4-122">hello 기본값은 '최신'입니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="a5bb4-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="a5bb4-123">settings.configuration.url</span></span> |<span data-ttu-id="a5bb4-124">string</span><span class="sxs-lookup"><span data-stu-id="a5bb4-124">string</span></span> |<span data-ttu-id="a5bb4-125">DSC 구성 zip 파일에서 어떤 toodownload hello URL 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="a5bb4-126">제공 된 hello URL 액세스에 대 한 SAS 토큰을 필요한 경우 SAS 토큰의 tooset hello protectedSettings.configurationUrlSasToken 속성 toohello 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="a5bb4-127">settings.configuration.script 및/또는 settings.configuration.function이 정의된 경우 이 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="a5bb4-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="a5bb4-128">settings.configuration.script</span></span> |<span data-ttu-id="a5bb4-129">string</span><span class="sxs-lookup"><span data-stu-id="a5bb4-129">string</span></span> |<span data-ttu-id="a5bb4-130">DSC 구성의 hello 정의 포함 하는 hello 스크립트의 hello 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="a5bb4-131">이 스크립트는 hello configuration.url 속성으로 지정 된 hello URL에서 다운로드 한 hello zip 파일의 hello 루트 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="a5bb4-132">settings.configuration.url 및/또는 settings.configuration.script가 정의된 경우 이 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="a5bb4-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="a5bb4-133">settings.configuration.function</span></span> |<span data-ttu-id="a5bb4-134">string</span><span class="sxs-lookup"><span data-stu-id="a5bb4-134">string</span></span> |<span data-ttu-id="a5bb4-135">DSC 구성의 hello 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="a5bb4-136">명명 된 hello 구성 configuration.script에 정의 된 hello 스크립트에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="a5bb4-137">settings.configuration.url 및/또는 settings.configuration.function이 정의된 경우 이 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="a5bb4-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a5bb4-138">settings.configurationArguments</span></span> |<span data-ttu-id="a5bb4-139">컬렉션</span><span class="sxs-lookup"><span data-stu-id="a5bb4-139">Collection</span></span> |<span data-ttu-id="a5bb4-140">Toopass tooyour DSC 구성을 원하는 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="a5bb4-141">이 속성은 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="a5bb4-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="a5bb4-142">settings.configurationData.url</span></span> |<span data-ttu-id="a5bb4-143">string</span><span class="sxs-lookup"><span data-stu-id="a5bb4-143">string</span></span> |<span data-ttu-id="a5bb4-144">DSC 구성에 대 한 입력으로 구성 데이터 (.psd1) 파일 toouse 어떤 toodownload에서 hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="a5bb4-145">제공 된 hello URL 액세스에 대 한 SAS 토큰을 필요한 경우 SAS 토큰의 tooset hello protectedSettings.configurationDataUrlSasToken 속성 toohello 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="a5bb4-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="a5bb4-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="a5bb4-147">문자열</span><span class="sxs-lookup"><span data-stu-id="a5bb4-147">string</span></span> |<span data-ttu-id="a5bb4-148">원격 분석 수집을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="a5bb4-149">hello 가능한 값만이 속성은 **'사용', '사용 안 함', ', 또는 $null**합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="a5bb4-150">이 속성을 비워 두거나 null로 설정하면 원격 분석이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="a5bb4-151">hello 기본값은 '.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-151">hello default value is ''.</span></span> [<span data-ttu-id="a5bb4-152">추가 정보</span><span class="sxs-lookup"><span data-stu-id="a5bb4-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="a5bb4-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="a5bb4-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="a5bb4-154">컬렉션</span><span class="sxs-lookup"><span data-stu-id="a5bb4-154">Collection</span></span> |<span data-ttu-id="a5bb4-155">어떤 toodownload에서 WMF를 hello 대체 위치를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="a5bb4-156">추가 정보</span><span class="sxs-lookup"><span data-stu-id="a5bb4-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="a5bb4-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a5bb4-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="a5bb4-158">컬렉션</span><span class="sxs-lookup"><span data-stu-id="a5bb4-158">Collection</span></span> |<span data-ttu-id="a5bb4-159">Toopass tooyour DSC 구성을 원하는 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="a5bb4-160">이 속성은 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-160">This property is encrypted.</span></span> |
| <span data-ttu-id="a5bb4-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a5bb4-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="a5bb4-162">string</span><span class="sxs-lookup"><span data-stu-id="a5bb4-162">string</span></span> |<span data-ttu-id="a5bb4-163">Configuration.url에 정의 된 hello SAS 토큰 tooaccess hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="a5bb4-164">이 속성은 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-164">This property is encrypted.</span></span> |
| <span data-ttu-id="a5bb4-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a5bb4-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="a5bb4-166">string</span><span class="sxs-lookup"><span data-stu-id="a5bb4-166">string</span></span> |<span data-ttu-id="a5bb4-167">ConfigurationData.url에 정의 된 hello SAS 토큰 tooaccess hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="a5bb4-168">이 속성은 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="a5bb4-169">Settings 및 ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="a5bb4-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="a5bb4-170">모든 설정이 hello VM에서 설정 텍스트 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="a5bb4-171">속성의 '설정' 공용 속성이 되므로 hello 설정 텍스트 파일에 암호화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="a5bb4-172">'ProtectedSettings' 속성의 인증서로 암호화 하 고 hello VM에서이 파일에 일반 텍스트로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="a5bb4-173">Hello 구성에서 자격 증명을 필요한 경우 protectedSettings 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="a5bb4-174">예제</span><span class="sxs-lookup"><span data-stu-id="a5bb4-174">Example</span></span>
<span data-ttu-id="a5bb4-175">hello 다음 예제에서는 파생 hello의 hello "시작" 섹션에서 [DSC 확장 처리기 개요 페이지](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="a5bb4-176">이 예제에서는 cmdlet toodeploy hello 확장명 대신 리소스 관리자 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="a5bb4-177">Hello "IisInstall.ps1" 구성을 저장에 배치할는 합니다. ZIP 파일 및 액세스할 수 있는 URL에 hello 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="a5bb4-178">이 예제에서는 Azure blob 저장소를 사용 하지만 가능한 toodownload. 임의의 위치에서 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="a5bb4-179">hello Azure 리소스 관리자 템플릿 hello 다음 코드 hello VM toodownload hello 올바른 파일 지시 고 hello 적절 한 PowerShell 함수를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="a5bb4-180">Hello 이전 형식에서 업데이트</span><span class="sxs-lookup"><span data-stu-id="a5bb4-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="a5bb4-181">Hello 이전 형식 (hello 공용 속성 ModulesUrl, ConfigurationFunction, SasToken, 또는 속성 포함) 자동으로 모든 설정은 toohello 현재 형식에 맞게 조정 하 고 이전과 마찬가지로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="a5bb4-182">스키마를 따르는 hello은 처럼 보이지만 어떤 hello 이전 설정 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-182">hello following schema is what hello previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
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
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

<span data-ttu-id="a5bb4-183">Hello 이전 형식 toohello 현재 형식에 맞게 변경 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="a5bb4-184">속성 이름</span><span class="sxs-lookup"><span data-stu-id="a5bb4-184">Property Name</span></span> | <span data-ttu-id="a5bb4-185">이전 스키마에 해당</span><span class="sxs-lookup"><span data-stu-id="a5bb4-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="a5bb4-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="a5bb4-186">settings.wmfVersion</span></span> |<span data-ttu-id="a5bb4-187">settings.WMFVersion</span><span class="sxs-lookup"><span data-stu-id="a5bb4-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="a5bb4-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="a5bb4-188">settings.configuration.url</span></span> |<span data-ttu-id="a5bb4-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="a5bb4-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="a5bb4-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="a5bb4-190">settings.configuration.script</span></span> |<span data-ttu-id="a5bb4-191">settings.ConfigurationFunction의 첫 번째 부분('\\\\' 앞)</span><span class="sxs-lookup"><span data-stu-id="a5bb4-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="a5bb4-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="a5bb4-192">settings.configuration.function</span></span> |<span data-ttu-id="a5bb4-193">settings.ConfigurationFunction의 두 번째 부분('\\\\' 뒤)</span><span class="sxs-lookup"><span data-stu-id="a5bb4-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="a5bb4-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a5bb4-194">settings.configurationArguments</span></span> |<span data-ttu-id="a5bb4-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="a5bb4-195">settings.Properties</span></span> |
| <span data-ttu-id="a5bb4-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="a5bb4-196">settings.configurationData.url</span></span> |<span data-ttu-id="a5bb4-197">protectedSettings.DataBlobUri(SAS 토큰 없이)</span><span class="sxs-lookup"><span data-stu-id="a5bb4-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="a5bb4-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="a5bb4-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="a5bb4-199">settings.Privacy.DataEnabled</span><span class="sxs-lookup"><span data-stu-id="a5bb4-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="a5bb4-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="a5bb4-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="a5bb4-201">settings.AdvancedOptions.DownloadMappings</span><span class="sxs-lookup"><span data-stu-id="a5bb4-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="a5bb4-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="a5bb4-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="a5bb4-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="a5bb4-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="a5bb4-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a5bb4-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="a5bb4-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="a5bb4-205">settings.SasToken</span></span> |
| <span data-ttu-id="a5bb4-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="a5bb4-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="a5bb4-207">protectedSettings.DataBlobUri의 SAS 토큰</span><span class="sxs-lookup"><span data-stu-id="a5bb4-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="a5bb4-208">문제 해결 - 오류 코드 1100</span><span class="sxs-lookup"><span data-stu-id="a5bb4-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="a5bb4-209">오류 코드 1100 hello 사용자 입력 toohello DSC 확장에 문제가 있다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="a5bb4-210">이러한 오류의 hello 텍스트는 가변적이 고 변경 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="a5bb4-211">다음은 몇 가지 발생할 수 있습니다 hello 오류와 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="a5bb4-212">잘못된 값</span><span class="sxs-lookup"><span data-stu-id="a5bb4-212">Invalid Values</span></span>
<span data-ttu-id="a5bb4-213">"Privacy.dataCollection이 '{0}'입니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="a5bb4-214">hello만 가능한 값은 ', '사용' 및 '해제' ""WmfVersion는 ' {'이 (0).</span><span class="sxs-lookup"><span data-stu-id="a5bb4-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="a5bb4-215">유일하게 가능한 값은 …</span><span class="sxs-lookup"><span data-stu-id="a5bb4-215">Only possible values are …</span></span> <span data-ttu-id="a5bb4-216">및 'latest'"</span><span class="sxs-lookup"><span data-stu-id="a5bb4-216">and 'latest'"</span></span>

<span data-ttu-id="a5bb4-217">문제점: 제공된 값이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="a5bb4-218">해결 방법: hello 잘못 된 값 tooa 유효한 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="a5bb4-219">Hello 세부 정보 섹션에서 hello 표를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="a5bb4-220">잘못된 URL</span><span class="sxs-lookup"><span data-stu-id="a5bb4-220">Invalid URL</span></span>
<span data-ttu-id="a5bb4-221">"ConfigurationData.url은 '{0}'입니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="a5bb4-222">유효한 URL이 아닙니다." "DataBlobUri는 '{0}'입니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="a5bb4-223">유효한 URL이 아닙니다." "Configuration.url이 '{0}'입니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="a5bb4-224">유효한 URL이 아닙니다."</span><span class="sxs-lookup"><span data-stu-id="a5bb4-224">This is not a valid URL"</span></span>

<span data-ttu-id="a5bb4-225">문제점: 제공된 URL이 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="a5bb4-226">해결 방법: 제공된 모든 URL을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="a5bb4-227">모든 Url hello 확장 hello 원격 컴퓨터에서 액세스할 수 있는 toovalid 위치를 확인 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="a5bb4-228">잘못된 ConfigurationArgument 형식</span><span class="sxs-lookup"><span data-stu-id="a5bb4-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="a5bb4-229">"잘못된 configurationArguments 형식 {0}입니다."</span><span class="sxs-lookup"><span data-stu-id="a5bb4-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="a5bb4-230">문제: hello ConfigurationArguments 속성 tooa 해시 테이블 개체를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="a5bb4-231">해결 방법: ConfigurationArguments 속성을 해시 테이블로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="a5bb4-232">Hello 앞에 있는 예제에서 제공 하는 hello 형식을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="a5bb4-233">따옴표, 쉼표 및 중괄호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="a5bb4-234">중복 ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="a5bb4-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="a5bb4-235">"공용 및 보호된 configurationArguments에 중복 인수 '{0}'이(가) 있습니다."</span><span class="sxs-lookup"><span data-stu-id="a5bb4-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="a5bb4-236">문제: 공용 설정에서 ConfigurationArguments hello hello ConfigurationArguments 보호 설정에 속성을 포함 hello로 이름이 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="a5bb4-237">해결 방법: hello 중복 된 속성 중 하나를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="a5bb4-238">누락된 속성</span><span class="sxs-lookup"><span data-stu-id="a5bb4-238">Missing Properties</span></span>
<span data-ttu-id="a5bb4-239">"Configuration.function을 사용하려면 configuration.url 또는 configuration.module을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="a5bb4-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="a5bb4-240">"Configuration.url을 사용하려면 configuration.script를 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="a5bb4-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="a5bb4-241">"Configuration.script를 사용하려면 configuration.url을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="a5bb4-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="a5bb4-242">"Configuration.url을 사용하려면 configuration.function을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="a5bb4-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="a5bb4-243">"ConfigurationUrlSasToken을 사용하려면 configuration.url을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="a5bb4-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="a5bb4-244">"ConfigurationDataUrlSasToken을 사용하려면 configurationData.url을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="a5bb4-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="a5bb4-245">문제점: 정의된 속성에 누락된 다른 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="a5bb4-246">해결 방법:</span><span class="sxs-lookup"><span data-stu-id="a5bb4-246">Solutions:</span></span> 

* <span data-ttu-id="a5bb4-247">Hello 누락 된 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-247">Provide hello missing property.</span></span>
* <span data-ttu-id="a5bb4-248">Hello 누락 된 속성이 되어야 하는 hello 속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5bb4-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5bb4-249">Next Steps</span></span>
<span data-ttu-id="a5bb4-250">DSC에 대해 알아보고에 설정 하는 가상 컴퓨터 크기 [hello Azure DSC 확장을 사용 하 여 가상 컴퓨터 크기 조정 집합 사용 하 여](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="a5bb4-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="a5bb4-251">[DSC의 보안 자격 증명 관리](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="a5bb4-252">Hello Azure DSC 확장 처리기에 대 한 자세한 내용은 참조 하십시오. [소개 toohello Azure 필요한 상태 구성 확장 처리기](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="a5bb4-253">PowerShell DSC에 대 한 자세한 내용은 [hello PowerShell 설명서 센터를 방문](https://msdn.microsoft.com/powershell/dsc/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5bb4-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

