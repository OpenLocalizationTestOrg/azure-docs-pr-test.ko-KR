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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿을 사용하여 Windows VMSS 및 원하는 상태 구성
이 문서에서는 hello에 대 한 hello 리소스 관리자 템플릿을 설명 [필요한 상태 구성 확장 처리기](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 

## <a name="template-example-for-a-windows-vm"></a>Windows VM의 템플릿 예제
hello 다음 코드 조각은 들어갑니다 hello hello 템플릿의 리소스 섹션.

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

## <a name="template-example-for-windows-vmss"></a>Windows VMSS의 템플릿 예제
VMSS 노드 "VirtualMachineProfile" hello "extensionProfile" 특성으로 "속성" 섹션을 있습니다. "extensions" 아래에 DSC가 추가됩니다. 

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

## <a name="detailed-settings-information"></a>자세한 설정 정보
hello 다음 스키마는 hello Azure Resource Manager 템플릿에 Azure DSC 확장의 hello 설정 부분입니다.

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

## <a name="details"></a>세부 정보
| 속성 이름 | 형식 | 설명 |
| --- | --- | --- |
| settings.wmfVersion |string |Hello VM에 설치 되어야 하는 Windows 관리 프레임 워크의 hello 버전을 지정 합니다. 이 속성 too'latest 설정 ' wmf hello 가장 업데이트 된 버전 설치 합니다. 이 속성에 대 한 hello 현재 가능한 값은 **'4.0', '5.0', ' 5.0PP' 및 'latest'**합니다. 이러한 가능한 값은 주체 tooupdates 합니다. hello 기본값은 '최신'입니다. |
| settings.configuration.url |string |DSC 구성 zip 파일에서 어떤 toodownload hello URL 위치를 지정합니다. 제공 된 hello URL 액세스에 대 한 SAS 토큰을 필요한 경우 SAS 토큰의 tooset hello protectedSettings.configurationUrlSasToken 속성 toohello 값이 필요 합니다. settings.configuration.script 및/또는 settings.configuration.function이 정의된 경우 이 속성이 필요합니다. |
| settings.configuration.script |string |DSC 구성의 hello 정의 포함 하는 hello 스크립트의 hello 파일 이름을 지정 합니다. 이 스크립트는 hello configuration.url 속성으로 지정 된 hello URL에서 다운로드 한 hello zip 파일의 hello 루트 폴더에 있어야 합니다. settings.configuration.url 및/또는 settings.configuration.script가 정의된 경우 이 속성이 필요합니다. |
| settings.configuration.function |string |DSC 구성의 hello 이름을 지정합니다. 명명 된 hello 구성 configuration.script에 정의 된 hello 스크립트에 포함 되어야 합니다. settings.configuration.url 및/또는 settings.configuration.function이 정의된 경우 이 속성이 필요합니다. |
| settings.configurationArguments |컬렉션 |Toopass tooyour DSC 구성을 원하는 매개 변수를 정의 합니다. 이 속성은 암호화되지 않습니다. |
| settings.configurationData.url |string |DSC 구성에 대 한 입력으로 구성 데이터 (.psd1) 파일 toouse 어떤 toodownload에서 hello URL을 지정 합니다. 제공 된 hello URL 액세스에 대 한 SAS 토큰을 필요한 경우 SAS 토큰의 tooset hello protectedSettings.configurationDataUrlSasToken 속성 toohello 값이 필요 합니다. |
| settings.privacy.dataEnabled |문자열 |원격 분석 수집을 사용하거나 사용하지 않도록 설정합니다. hello 가능한 값만이 속성은 **'사용', '사용 안 함', ', 또는 $null**합니다. 이 속성을 비워 두거나 null로 설정하면 원격 분석이 사용됩니다. hello 기본값은 '. [추가 정보](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |컬렉션 |어떤 toodownload에서 WMF를 hello 대체 위치를 정의 합니다. [추가 정보](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |컬렉션 |Toopass tooyour DSC 구성을 원하는 매개 변수를 정의 합니다. 이 속성은 암호화됩니다. |
| protectedSettings.configurationUrlSasToken |string |Configuration.url에 정의 된 hello SAS 토큰 tooaccess hello URL을 지정 합니다. 이 속성은 암호화됩니다. |
| protectedSettings.configurationDataUrlSasToken |string |ConfigurationData.url에 정의 된 hello SAS 토큰 tooaccess hello URL을 지정 합니다. 이 속성은 암호화됩니다. |

## <a name="settings-vs-protectedsettings"></a>Settings 및 ProtectedSettings
모든 설정이 hello VM에서 설정 텍스트 파일에 저장 됩니다.
속성의 '설정' 공용 속성이 되므로 hello 설정 텍스트 파일에 암호화 되지 않습니다.
'ProtectedSettings' 속성의 인증서로 암호화 하 고 hello VM에서이 파일에 일반 텍스트로 표시 되지 않습니다.

Hello 구성에서 자격 증명을 필요한 경우 protectedSettings 포함 될 수 있습니다.

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

## <a name="example"></a>예제
hello 다음 예제에서는 파생 hello의 hello "시작" 섹션에서 [DSC 확장 처리기 개요 페이지](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
이 예제에서는 cmdlet toodeploy hello 확장명 대신 리소스 관리자 템플릿을 사용 합니다. Hello "IisInstall.ps1" 구성을 저장에 배치할는 합니다. ZIP 파일 및 액세스할 수 있는 URL에 hello 파일을 업로드 합니다. 이 예제에서는 Azure blob 저장소를 사용 하지만 가능한 toodownload. 임의의 위치에서 ZIP 파일입니다.

hello Azure 리소스 관리자 템플릿 hello 다음 코드 hello VM toodownload hello 올바른 파일 지시 고 hello 적절 한 PowerShell 함수를 실행 합니다.

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

## <a name="updating-from-hello-previous-format"></a>Hello 이전 형식에서 업데이트
Hello 이전 형식 (hello 공용 속성 ModulesUrl, ConfigurationFunction, SasToken, 또는 속성 포함) 자동으로 모든 설정은 toohello 현재 형식에 맞게 조정 하 고 이전과 마찬가지로 실행 합니다.

스키마를 따르는 hello은 처럼 보이지만 어떤 hello 이전 설정 스키마입니다.

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

Hello 이전 형식 toohello 현재 형식에 맞게 변경 다음과 같습니다.

| 속성 이름 | 이전 스키마에 해당 |
| --- | --- |
| settings.wmfVersion |settings.WMFVersion |
| settings.configuration.url |settings.ModulesUrl |
| settings.configuration.script |settings.ConfigurationFunction의 첫 번째 부분('\\\\' 앞) |
| settings.configuration.function |settings.ConfigurationFunction의 두 번째 부분('\\\\' 뒤) |
| settings.configurationArguments |settings.Properties |
| settings.configurationData.url |protectedSettings.DataBlobUri(SAS 토큰 없이) |
| settings.privacy.dataEnabled |settings.Privacy.DataEnabled |
| settings.advancedOptions.downloadMappings |settings.AdvancedOptions.DownloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |settings.SasToken |
| protectedSettings.configurationDataUrlSasToken |protectedSettings.DataBlobUri의 SAS 토큰 |

## <a name="troubleshooting---error-code-1100"></a>문제 해결 - 오류 코드 1100
오류 코드 1100 hello 사용자 입력 toohello DSC 확장에 문제가 있다는 것을 나타냅니다.
이러한 오류의 hello 텍스트는 가변적이 고 변경 될 수 있습니다.
다음은 몇 가지 발생할 수 있습니다 hello 오류와 해결 방법입니다.

### <a name="invalid-values"></a>잘못된 값
"Privacy.dataCollection이 '{0}'입니다. hello만 가능한 값은 ', '사용' 및 '해제' ""WmfVersion는 ' {'이 (0). 유일하게 가능한 값은 … 및 'latest'"

문제점: 제공된 값이 허용되지 않습니다.

해결 방법: hello 잘못 된 값 tooa 유효한 값을 변경 합니다. Hello 세부 정보 섹션에서 hello 표를 참조 하세요.

### <a name="invalid-url"></a>잘못된 URL
"ConfigurationData.url은 '{0}'입니다. 유효한 URL이 아닙니다." "DataBlobUri는 '{0}'입니다. 유효한 URL이 아닙니다." "Configuration.url이 '{0}'입니다. 유효한 URL이 아닙니다."

문제점: 제공된 URL이 유효하지 않습니다.

해결 방법: 제공된 모든 URL을 확인합니다. 모든 Url hello 확장 hello 원격 컴퓨터에서 액세스할 수 있는 toovalid 위치를 확인 하 고 있는지 확인 합니다.

### <a name="invalid-configurationargument-type"></a>잘못된 ConfigurationArgument 형식
"잘못된 configurationArguments 형식 {0}입니다."

문제: hello ConfigurationArguments 속성 tooa 해시 테이블 개체를 확인할 수 없습니다. 

해결 방법: ConfigurationArguments 속성을 해시 테이블로 만듭니다. Hello 앞에 있는 예제에서 제공 하는 hello 형식을 따라야 합니다. 따옴표, 쉼표 및 중괄호를 확인합니다.

### <a name="duplicate-configurationarguments"></a>중복 ConfigurationArguments
"공용 및 보호된 configurationArguments에 중복 인수 '{0}'이(가) 있습니다."

문제: 공용 설정에서 ConfigurationArguments hello hello ConfigurationArguments 보호 설정에 속성을 포함 hello로 이름이 같은 합니다.

해결 방법: hello 중복 된 속성 중 하나를 제거 합니다.

### <a name="missing-properties"></a>누락된 속성
"Configuration.function을 사용하려면 configuration.url 또는 configuration.module을 지정해야 합니다."

"Configuration.url을 사용하려면 configuration.script를 지정해야 합니다."

"Configuration.script를 사용하려면 configuration.url을 지정해야 합니다."

"Configuration.url을 사용하려면 configuration.function을 지정해야 합니다."

"ConfigurationUrlSasToken을 사용하려면 configuration.url을 지정해야 합니다."

"ConfigurationDataUrlSasToken을 사용하려면 configurationData.url을 지정해야 합니다."

문제점: 정의된 속성에 누락된 다른 속성이 필요합니다.

해결 방법: 

* Hello 누락 된 속성을 제공 합니다.
* Hello 누락 된 속성이 되어야 하는 hello 속성을 제거 합니다.

## <a name="next-steps"></a>다음 단계
DSC에 대해 알아보고에 설정 하는 가상 컴퓨터 크기 [hello Azure DSC 확장을 사용 하 여 가상 컴퓨터 크기 조정 집합 사용 하 여](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

[DSC의 보안 자격 증명 관리](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 자세한 내용을 참조하세요. 

Hello Azure DSC 확장 처리기에 대 한 자세한 내용은 참조 하십시오. [소개 toohello Azure 필요한 상태 구성 확장 처리기](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 

PowerShell DSC에 대 한 자세한 내용은 [hello PowerShell 설명서 센터를 방문](https://msdn.microsoft.com/powershell/dsc/overview)합니다. 

