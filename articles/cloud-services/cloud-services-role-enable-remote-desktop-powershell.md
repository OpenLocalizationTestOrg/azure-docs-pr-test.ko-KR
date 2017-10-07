---
title: "aaaEnable PowerShell을 사용 하 여 Azure 클라우드 서비스에서 역할에 대 한 원격 데스크톱 연결"
description: "어떻게 tooconfigure azure 클라우드 PowerShell tooallow 원격 데스크톱 연결을 사용 하 여 서비스 응용 프로그램"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>PowerShell을 사용하여 Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure 클래식 포털](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

원격 데스크톱 사용 하면 Azure에서 실행 중인 역할의 tooaccess hello 데스크톱 있습니다. 원격 데스크톱 연결 tootroubleshoot를 사용할 수 있으며 실행 되는 동안 응용 프로그램 문제를 진단할 수 있습니다.

이 문서에서는 설명 방법을 PowerShell을 사용 하 여 클라우드 서비스 역할에 원격 데스크톱 tooenable 합니다. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello이이 문서에 필요한 필수 구성 요소에 대 한 합니다. Hello 응용 프로그램 배포 된 후 원격 데스크톱을 사용할 수 있도록 PowerShell에서 원격 데스크톱 확장 hello를 사용 합니다.

## <a name="configure-remote-desktop-from-powershell"></a>PowerShell에서 원격 데스크톱 구성
hello [집합 AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet는 지정 된 역할 또는 클라우드 서비스 배포의 모든 역할에 원격 데스크톱 tooenable 허용 합니다. hello cmdlet을 사용 하면 hello hello 통해 원격 데스크톱 사용자에 대 한 hello 사용자 이름 및 암호를 지정 하면 *자격 증명* PSCredential 개체를 받는 매개 변수입니다.

Hello를 호출 하 여 hello PSCredential 개체를 쉽게 설정할 수 PowerShell 대화형으로 사용 하는 경우 [자격 증명 가져오기](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

```
$remoteusercredentials = Get-Credential
```

이 명령은 tooenter hello 사용자 이름과 암호 hello 원격 사용자를 안전 하 게에서 허용 대화 상자를 표시 합니다.

Hello를 설정할 수 있으므로 PowerShell 자동화 시나리오에 유용 합니다 **PSCredential** 사용자 상호 작용이 필요 하지 않은 방식으로 개체입니다. 첫째, tooset 보안 암호 구성 해야 합니다. Tooa 보안 문자열로 변환할 일반 텍스트 암호를 지정 하 여 시작 하기를 사용 하 여 [Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)합니다. 다음 해야 tooconvert이 보안 문자열 사용 하 여 암호화 된 표준 문자열 [Convertfrom-securestring](https://technet.microsoft.com/library/hh849814.aspx)합니다. 이 암호화 된 표준 문자열 tooa 사용 하 여 파일을 저장할 수 이제 [Set-content](https://technet.microsoft.com/library/ee176959.aspx)합니다.

또한 tootype에에서 없는 hello 암호 될 때마다 있도록 보안 암호 파일을 만들 수 있습니다. 보안 암호 파일은 일반 텍스트 파일보다 더 좋습니다. 다음 PowerShell toocreate 보안 암호 파일 hello를 사용 합니다.

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> Hello 암호를 설정할 때는 hello를 충족 하는지 확인 [복잡성 요구 사항을](https://technet.microsoft.com/library/cc786468.aspx)합니다.
>
>

hello 보안 암호 파일에서 toocreate hello 자격 증명 개체를 hello 파일 내용을 읽고 해야 변환할 백 tooa 사용 하 여 문자열을 보안 [Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)합니다.

hello [집합 AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet도 허용는 *만료* 매개 변수를 지정 하는 한 **DateTime** hello 사용자 계정이 만료 합니다. 예를 들어 설정할 수 있습니다 hello 계정 tooexpire 몇 일 동안 hello 현재 날짜와 시간에서.

PowerShell 예제 tooset 클라우드 서비스에 원격 데스크톱 확장을 hello 하는 방법을 보여 줍니다.

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
또한 필요에 따라 hello 배포 슬롯 및 tooenable 원격 데스크톱에서 원하는 역할을 지정할 수 있습니다. Hello cmdlet hello에서 모든 역할에 원격 데스크톱을 사용 하면 이러한 매개 변수를 지정 하지 않은 경우 **프로덕션** 배포 슬롯입니다.

원격 데스크톱 확장 hello 배포와 연결 됩니다. Hello 서비스에 대 한 새 배포를 만드는 경우 해당 배포에 tooenable 원격 데스크톱을가 있습니다. 항상 toohave 원격 데스크톱 사용 하도록 설정 하려면, hello PowerShell 스크립트를 배포 워크플로에 통합 고려해 야 합니다.

## <a name="remote-desktop-into-a-role-instance"></a>원격 데스크톱을 역할 인스턴스로 가져오기
hello [Get-azureremotedesktopfile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet은 사용 되는 tooremote 데스크톱을 사용 하 여 클라우드 서비스의 특정 역할 인스턴스. Hello를 사용할 수 있습니다 *LocalPath* 매개 변수 toodownload hello RDP 파일을 로컬입니다. Hello를 사용할 수 있습니다 또는 *시작* 매개 변수 toodirectly 시작 hello 원격 데스크톱 연결 대화 tooaccess hello 클라우드 서비스 역할 인스턴스.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>서비스에서 원격 데스크톱 확장을 사용할 수 있는지 확인합니다.
hello [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet을 표시 하는 원격 데스크톱 설정 또는 서비스 배포에서 수행 되지 않습니다. hello cmdlet에는 원격 데스크톱 사용자 hello 및 원격 데스크톱 확장 hello를 사용 하는 hello 역할에 대 한 hello 사용자 이름을 반환 합니다. 기본적으로이 hello 배포 슬롯에서 발생 하 고 대신 슬롯 준비 toouse hello를 선택할 수 있습니다.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>서비스에서 원격 데스크톱 확장 제거
이미 활성화 된 배포에서 원격 데스크톱 확장 hello tooupdate hello 필요한 원격 데스크톱 설정 하는 경우 먼저 hello 확장을 제거 합니다. 고 hello 새 설정으로 다시 설정 합니다. 예를 들어 tooset 하려는 경우 hello 원격 사용자 계정 또는 hello 계정에 대 한 새 암호를 만료 되었습니다. 이 작업을 수행 hello 원격 데스크톱 확장을 사용 하는 기존 배포에 필요 합니다. 새 배포를 위해 적용할 수 있습니다 단순히 hello 확장 직접.

tooremove hello 원격 데스크톱 확장 hello 배포에서 hello를 사용할 수 있습니다 [제거 AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet. 또한 필요에 따라 hello 배포 슬롯 및 tooremove hello 원격 데스크톱 확장 하려는 역할을 지정할 수 있습니다.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> 호출 해야 hello toocompletely 제거 hello 확장 구성 *제거* hello 사용 하 여 cmdlet **UninstallConfiguration** 매개 변수입니다.
>
> hello **UninstallConfiguration** 모든 확장 구성을 제거 하는 매개 변수 즉 toohello 적용 된 서비스입니다. 모든 확장 구성 hello 서비스 구성에 연관 되어 있습니다. 호출 hello *제거* 없이 cmdlet **UninstallConfiguration** hello 연결을 끊습니다 <mark>배포</mark> hello 확장 구성에서 효과적으로 제거 hello 확장입니다. 그러나 hello 확장 구성을 유지 hello 서비스와 연결 됩니다.
>
>

## <a name="additional-resources"></a>추가 리소스

[어떻게 tooConfigure 클라우드 서비스](cloud-services-how-to-configure.md)
[클라우드 서비스 FAQ-원격 데스크톱](cloud-services-faq.md)
