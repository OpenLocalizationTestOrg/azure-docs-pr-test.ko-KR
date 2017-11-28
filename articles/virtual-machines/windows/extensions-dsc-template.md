---
title: "원하는 상태 구성 Resource Manager 템플릿 | Microsoft Docs"
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
ms.openlocfilehash: 4292f9d8cd181073fdf0adff99fcb9624e0e9f55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="f88a7-103">Azure Resource Manager 템플릿을 사용하여 Windows VMSS 및 원하는 상태 구성</span><span class="sxs-lookup"><span data-stu-id="f88a7-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="f88a7-104">이 문서에서는 [필요한 상태 구성 확장 처리기](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 위한 Resource Manager 템플릿에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-104">This article describes the Resource Manager template for the [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="f88a7-105">Windows VM의 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="f88a7-105">Template example for a Windows VM</span></span>
<span data-ttu-id="f88a7-106">다음 코드 조각은 템플릿의 리소스 섹션에 대한 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-106">The following snippet goes into the Resource section of the template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="f88a7-107">Windows VMSS의 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="f88a7-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="f88a7-108">VMSS 노드에는 "VirtualMachineProfile", "extensionProfile" 특성을 포함하는 "properties" 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-108">A VMSS node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="f88a7-109">"extensions" 아래에 DSC가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="f88a7-110">자세한 설정 정보</span><span class="sxs-lookup"><span data-stu-id="f88a7-110">Detailed Settings Information</span></span>
<span data-ttu-id="f88a7-111">다음 스키마는 Azure Resource Manager 템플릿에 있는 Azure DSC 확장의 설정 부분에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-111">The following schema is for the settings portion of the Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="f88a7-112">세부 정보</span><span class="sxs-lookup"><span data-stu-id="f88a7-112">Details</span></span>
| <span data-ttu-id="f88a7-113">속성 이름</span><span class="sxs-lookup"><span data-stu-id="f88a7-113">Property Name</span></span> | <span data-ttu-id="f88a7-114">형식</span><span class="sxs-lookup"><span data-stu-id="f88a7-114">Type</span></span> | <span data-ttu-id="f88a7-115">설명</span><span class="sxs-lookup"><span data-stu-id="f88a7-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f88a7-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="f88a7-116">settings.wmfVersion</span></span> |<span data-ttu-id="f88a7-117">문자열</span><span class="sxs-lookup"><span data-stu-id="f88a7-117">string</span></span> |<span data-ttu-id="f88a7-118">VM에 설치해야 하는 Windows Management Framework의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-118">Specifies the version of the Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="f88a7-119">이 속성을 'latest'로 설정하면 WMF의 최신 업데이트 버전이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-119">Setting this property to 'latest' installs the most updated version of WMF.</span></span> <span data-ttu-id="f88a7-120">현재 이 속성에 대해 설정 가능한 값은 **'4.0', '5.0', '5.0PP' 및 'latest'**뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-120">The only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="f88a7-121">가능한 값은 업데이트에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-121">These possible values are subject to updates.</span></span> <span data-ttu-id="f88a7-122">기본값은 'latest'입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-122">The default value is 'latest'.</span></span> |
| <span data-ttu-id="f88a7-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="f88a7-123">settings.configuration.url</span></span> |<span data-ttu-id="f88a7-124">문자열</span><span class="sxs-lookup"><span data-stu-id="f88a7-124">string</span></span> |<span data-ttu-id="f88a7-125">DSC 구성 zip 파일을 다운로드할 URL 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-125">Specifies the URL location from which to download your DSC configuration zip file.</span></span> <span data-ttu-id="f88a7-126">제공된 URL에서 액세스를 위해 SAS 토큰을 요구하는 경우 protectedSettings.configurationUrlSasToken 속성을 SAS 토큰 값으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-126">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationUrlSasToken property to the value of your SAS token.</span></span> <span data-ttu-id="f88a7-127">settings.configuration.script 및/또는 settings.configuration.function이 정의된 경우 이 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="f88a7-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="f88a7-128">settings.configuration.script</span></span> |<span data-ttu-id="f88a7-129">문자열</span><span class="sxs-lookup"><span data-stu-id="f88a7-129">string</span></span> |<span data-ttu-id="f88a7-130">DSC 구성의 정의를 포함하는 스크립트의 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-130">Specifies the file name of the script that contains the definition of your DSC configuration.</span></span> <span data-ttu-id="f88a7-131">이 스크립트는 configuration.url 속성에 지정된 URL에서 다운로드된 zip 파일의 루트 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-131">This script must be in the root folder of the zip file downloaded from the URL specified by the configuration.url property.</span></span> <span data-ttu-id="f88a7-132">settings.configuration.url 및/또는 settings.configuration.script가 정의된 경우 이 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="f88a7-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="f88a7-133">settings.configuration.function</span></span> |<span data-ttu-id="f88a7-134">문자열</span><span class="sxs-lookup"><span data-stu-id="f88a7-134">string</span></span> |<span data-ttu-id="f88a7-135">DSC 구성의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-135">Specifies the name of your DSC configuration.</span></span> <span data-ttu-id="f88a7-136">명명된 구성은 configuration.script에 정의된 스크립트에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-136">The configuration named must be contained in the script defined by configuration.script.</span></span> <span data-ttu-id="f88a7-137">settings.configuration.url 및/또는 settings.configuration.function이 정의된 경우 이 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="f88a7-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="f88a7-138">settings.configurationArguments</span></span> |<span data-ttu-id="f88a7-139">컬렉션</span><span class="sxs-lookup"><span data-stu-id="f88a7-139">Collection</span></span> |<span data-ttu-id="f88a7-140">DSC 구성을 전달하려는 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-140">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="f88a7-141">이 속성은 암호화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="f88a7-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="f88a7-142">settings.configurationData.url</span></span> |<span data-ttu-id="f88a7-143">문자열</span><span class="sxs-lookup"><span data-stu-id="f88a7-143">string</span></span> |<span data-ttu-id="f88a7-144">DSC 구성에 대한 입력으로 사용할 구성 데이터(.psd1) 파일을 다운로드할 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-144">Specifies the URL from which to download your configuration data (.psd1) file to use as input for your DSC configuration.</span></span> <span data-ttu-id="f88a7-145">제공된 URL에서 액세스를 위해 SAS 토큰을 요구하는 경우 protectedSettings.configurationDataUrlSasToken 속성을 SAS 토큰 값으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-145">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationDataUrlSasToken property to the value of your SAS token.</span></span> |
| <span data-ttu-id="f88a7-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="f88a7-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="f88a7-147">문자열</span><span class="sxs-lookup"><span data-stu-id="f88a7-147">string</span></span> |<span data-ttu-id="f88a7-148">원격 분석 수집을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="f88a7-149">이 속성에 설정할 수 있는 값은 **'Enable', 'Disable', '' 또는 $null**뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-149">The only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="f88a7-150">이 속성을 비워 두거나 null로 설정하면 원격 분석이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="f88a7-151">기본값은 ''입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-151">The default value is ''.</span></span> [<span data-ttu-id="f88a7-152">추가 정보</span><span class="sxs-lookup"><span data-stu-id="f88a7-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="f88a7-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="f88a7-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="f88a7-154">컬렉션</span><span class="sxs-lookup"><span data-stu-id="f88a7-154">Collection</span></span> |<span data-ttu-id="f88a7-155">WMF를 다운로드할 대체 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-155">Defines alternate locations from which to download the WMF.</span></span> [<span data-ttu-id="f88a7-156">추가 정보</span><span class="sxs-lookup"><span data-stu-id="f88a7-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="f88a7-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="f88a7-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="f88a7-158">컬렉션</span><span class="sxs-lookup"><span data-stu-id="f88a7-158">Collection</span></span> |<span data-ttu-id="f88a7-159">DSC 구성을 전달하려는 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-159">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="f88a7-160">이 속성은 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-160">This property is encrypted.</span></span> |
| <span data-ttu-id="f88a7-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="f88a7-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="f88a7-162">문자열</span><span class="sxs-lookup"><span data-stu-id="f88a7-162">string</span></span> |<span data-ttu-id="f88a7-163">configuration.url에서 정의한 URL에 액세스하기 위해 SAS 토큰을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-163">Specifies the SAS token to access the URL defined by configuration.url.</span></span> <span data-ttu-id="f88a7-164">이 속성은 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-164">This property is encrypted.</span></span> |
| <span data-ttu-id="f88a7-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="f88a7-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="f88a7-166">문자열</span><span class="sxs-lookup"><span data-stu-id="f88a7-166">string</span></span> |<span data-ttu-id="f88a7-167">configuration.url에서 정의한 URL에 액세스하기 위해 SAS 토큰을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-167">Specifies the SAS token to access the URL defined by configurationData.url.</span></span> <span data-ttu-id="f88a7-168">이 속성은 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="f88a7-169">Settings 및 ProtectedSettings</span><span class="sxs-lookup"><span data-stu-id="f88a7-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="f88a7-170">모든 설정은 VM의 설정 텍스트 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-170">All settings are saved in a settings text file on the VM.</span></span>
<span data-ttu-id="f88a7-171">'settings'의 속성은 설정 텍스트 파일에서 암호화되지 않으므로 공용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-171">Properties under 'settings' are public properties because they are not encrypted in the settings text file.</span></span>
<span data-ttu-id="f88a7-172">'protectedSettings'의 속성은 인증서를 사용하여 암호화되므로 VM에서 이 파일에 일반 텍스트로 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on the VM.</span></span>

<span data-ttu-id="f88a7-173">구성에 자격 증명이 필요한 경우 protectedSettings에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-173">If the configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="f88a7-174">예</span><span class="sxs-lookup"><span data-stu-id="f88a7-174">Example</span></span>
<span data-ttu-id="f88a7-175">다음 예제는 [DSC 확장 처리기 개요 페이지](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)의 "시작" 섹션에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-175">The following example derives from the "Getting Started" section of the [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="f88a7-176">이 예제에서는 cmdlet 대신 Resource Manager 템플릿을 사용하여 확장을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-176">This example uses Resource Manager templates instead of cmdlets to deploy the extension.</span></span> <span data-ttu-id="f88a7-177">"IisInstall.ps1" 구성을 저장하고 .ZIP 파일에 배치한 다음 파일을 액세스 가능한 URL에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-177">Save the "IisInstall.ps1" configuration, place it in a .ZIP file, and upload the file in an accessible URL.</span></span> <span data-ttu-id="f88a7-178">이 예제에서는 Azure Blob Storage를 사용하지만 임의의 위치에서 .ZIP 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-178">This example uses Azure blob storage, but it is possible to download .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="f88a7-179">Azure Resource Manager 템플릿에서 다음 코드는 VM에 올바른 파일을 다운로드하고 적절한 PowerShell 함수를 실행하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-179">In the Azure Resource Manager template, the following code instructs the VM to download the correct file and run the appropriate PowerShell function:</span></span>

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

## <a name="updating-from-the-previous-format"></a><span data-ttu-id="f88a7-180">이전 형식에서 업데이트</span><span class="sxs-lookup"><span data-stu-id="f88a7-180">Updating from the Previous Format</span></span>
<span data-ttu-id="f88a7-181">이전 형식의 모든 설정(공용 속성 ModulesUrl, ConfigurationFunction, SasToken 또는 Properties 포함)은 현재 형식으로 자동 조정되며 이전과 같이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-181">Any settings in the previous format (containing the public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt to the current format and run just as they did before.</span></span>

<span data-ttu-id="f88a7-182">다음 스키마는 이전 설정 스키마와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-182">The following schema is what the previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points to private Azure Blob Storage",
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

<span data-ttu-id="f88a7-183">다음은 현재 형식에 맞게 이전 형식을 조정하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-183">Here's how the previous format adapts to the current format:</span></span>

| <span data-ttu-id="f88a7-184">속성 이름</span><span class="sxs-lookup"><span data-stu-id="f88a7-184">Property Name</span></span> | <span data-ttu-id="f88a7-185">이전 스키마에 해당</span><span class="sxs-lookup"><span data-stu-id="f88a7-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="f88a7-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="f88a7-186">settings.wmfVersion</span></span> |<span data-ttu-id="f88a7-187">settings.WMFVersion</span><span class="sxs-lookup"><span data-stu-id="f88a7-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="f88a7-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="f88a7-188">settings.configuration.url</span></span> |<span data-ttu-id="f88a7-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="f88a7-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="f88a7-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="f88a7-190">settings.configuration.script</span></span> |<span data-ttu-id="f88a7-191">settings.ConfigurationFunction의 첫 번째 부분('\\\\' 앞)</span><span class="sxs-lookup"><span data-stu-id="f88a7-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="f88a7-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="f88a7-192">settings.configuration.function</span></span> |<span data-ttu-id="f88a7-193">settings.ConfigurationFunction의 두 번째 부분('\\\\' 뒤)</span><span class="sxs-lookup"><span data-stu-id="f88a7-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="f88a7-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="f88a7-194">settings.configurationArguments</span></span> |<span data-ttu-id="f88a7-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="f88a7-195">settings.Properties</span></span> |
| <span data-ttu-id="f88a7-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="f88a7-196">settings.configurationData.url</span></span> |<span data-ttu-id="f88a7-197">protectedSettings.DataBlobUri(SAS 토큰 없이)</span><span class="sxs-lookup"><span data-stu-id="f88a7-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="f88a7-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="f88a7-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="f88a7-199">settings.Privacy.DataEnabled</span><span class="sxs-lookup"><span data-stu-id="f88a7-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="f88a7-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="f88a7-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="f88a7-201">settings.AdvancedOptions.DownloadMappings</span><span class="sxs-lookup"><span data-stu-id="f88a7-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="f88a7-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="f88a7-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="f88a7-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="f88a7-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="f88a7-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="f88a7-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="f88a7-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="f88a7-205">settings.SasToken</span></span> |
| <span data-ttu-id="f88a7-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="f88a7-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="f88a7-207">protectedSettings.DataBlobUri의 SAS 토큰</span><span class="sxs-lookup"><span data-stu-id="f88a7-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="f88a7-208">문제 해결 - 오류 코드 1100</span><span class="sxs-lookup"><span data-stu-id="f88a7-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="f88a7-209">오류 코드 1100은 DSC 확장에 대한 사용자 입력에 문제가 있다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-209">Error Code 1100 indicates that there is a problem with the user input to the DSC extension.</span></span>
<span data-ttu-id="f88a7-210">이러한 오류의 텍스트는 변수이며 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-210">The text of these errors is variable and may change.</span></span>
<span data-ttu-id="f88a7-211">다음은 발생할 수 있는 일부 오류와 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-211">Here are some of the errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="f88a7-212">잘못된 값</span><span class="sxs-lookup"><span data-stu-id="f88a7-212">Invalid Values</span></span>
<span data-ttu-id="f88a7-213">"Privacy.dataCollection이 '{0}'입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="f88a7-214">유일하게 가능한 값은 '', 'Enable' 및 'Disable'" 이며 "WmfVersion은 '{0}'입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-214">The only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="f88a7-215">유일하게 가능한 값은 …</span><span class="sxs-lookup"><span data-stu-id="f88a7-215">Only possible values are …</span></span> <span data-ttu-id="f88a7-216">및 'latest'"</span><span class="sxs-lookup"><span data-stu-id="f88a7-216">and 'latest'"</span></span>

<span data-ttu-id="f88a7-217">문제점: 제공된 값이 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="f88a7-218">해결 방법: 잘못된 값을 올바른 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-218">Solution: Change the invalid value to a valid value.</span></span> <span data-ttu-id="f88a7-219">세부 정보 섹션의 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f88a7-219">See the table in the Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="f88a7-220">잘못된 URL</span><span class="sxs-lookup"><span data-stu-id="f88a7-220">Invalid URL</span></span>
<span data-ttu-id="f88a7-221">"ConfigurationData.url은 '{0}'입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="f88a7-222">유효한 URL이 아닙니다." "DataBlobUri는 '{0}'입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="f88a7-223">유효한 URL이 아닙니다." "Configuration.url이 '{0}'입니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="f88a7-224">유효한 URL이 아닙니다."</span><span class="sxs-lookup"><span data-stu-id="f88a7-224">This is not a valid URL"</span></span>

<span data-ttu-id="f88a7-225">문제점: 제공된 URL이 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="f88a7-226">해결 방법: 제공된 모든 URL을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="f88a7-227">모든 URL이 원격 컴퓨터의 확장 기능에서 액세스할 수 있는 올바른 위치인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-227">Make sure all URLs resolve to valid locations that the extension can access on the remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="f88a7-228">잘못된 ConfigurationArgument 형식</span><span class="sxs-lookup"><span data-stu-id="f88a7-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="f88a7-229">"잘못된 configurationArguments 형식 {0}입니다."</span><span class="sxs-lookup"><span data-stu-id="f88a7-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="f88a7-230">문제점: ConfigurationArguments 속성을 Hashtable 개체로 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-230">Problem: The ConfigurationArguments property cannot resolve to a Hashtable object.</span></span> 

<span data-ttu-id="f88a7-231">해결 방법: ConfigurationArguments 속성을 해시 테이블로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="f88a7-232">위의 예제에서 제공한 형식을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-232">Follow the format provided in the preceeding example.</span></span> <span data-ttu-id="f88a7-233">따옴표, 쉼표 및 중괄호를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="f88a7-234">중복 ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="f88a7-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="f88a7-235">"공용 및 보호된 configurationArguments에 중복 인수 '{0}'이(가) 있습니다."</span><span class="sxs-lookup"><span data-stu-id="f88a7-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="f88a7-236">문제점: 공용 설정의 ConfigurationArguments 및 보호된 설정의 ConfigurationArguments에 동일한 이름의 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-236">Problem: The ConfigurationArguments in public settings and the ConfigurationArguments in protected settings contain properties with the same name.</span></span>

<span data-ttu-id="f88a7-237">해결 방법: 중복된 속성 중 하나를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-237">Solution: Remove one of the duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="f88a7-238">누락된 속성</span><span class="sxs-lookup"><span data-stu-id="f88a7-238">Missing Properties</span></span>
<span data-ttu-id="f88a7-239">"Configuration.function을 사용하려면 configuration.url 또는 configuration.module을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="f88a7-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="f88a7-240">"Configuration.url을 사용하려면 configuration.script를 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="f88a7-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="f88a7-241">"Configuration.script를 사용하려면 configuration.url을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="f88a7-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="f88a7-242">"Configuration.url을 사용하려면 configuration.function을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="f88a7-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="f88a7-243">"ConfigurationUrlSasToken을 사용하려면 configuration.url을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="f88a7-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="f88a7-244">"ConfigurationDataUrlSasToken을 사용하려면 configurationData.url을 지정해야 합니다."</span><span class="sxs-lookup"><span data-stu-id="f88a7-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="f88a7-245">문제점: 정의된 속성에 누락된 다른 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="f88a7-246">해결 방법:</span><span class="sxs-lookup"><span data-stu-id="f88a7-246">Solutions:</span></span> 

* <span data-ttu-id="f88a7-247">누락된 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-247">Provide the missing property.</span></span>
* <span data-ttu-id="f88a7-248">누락된 속성을 요구하는 속성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f88a7-248">Remove the property that needs the missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f88a7-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f88a7-249">Next Steps</span></span>
<span data-ttu-id="f88a7-250">[Azure DSC 확장에 가상 컴퓨터 확장 집합 사용](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)에서 DSC 및 가상 컴퓨터 확장 집합에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f88a7-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="f88a7-251">[DSC의 보안 자격 증명 관리](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f88a7-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="f88a7-252">Azure DSC 확장 처리기에 대한 자세한 내용은 [Azure 필요한 상태 구성 확장 처리기 소개](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f88a7-252">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="f88a7-253">PowerShell DSC에 대한 자세한 내용은 [PowerShell 설명서 센터를 방문하세요](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="f88a7-253">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

