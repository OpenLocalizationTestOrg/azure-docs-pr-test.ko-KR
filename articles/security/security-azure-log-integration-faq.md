---
title: "로그 통합 FAQ aaaAzure | Microsoft Docs"
description: "이 문서는 Azure 로그 통합에 대한 질문에 답변합니다."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a>Azure 로그 통합 FAQ
이 문서는 Azure 로그 통합에 대한 FAQ(질문과 대답)입니다. 

Azure 로그 통합은 Windows 운영 체제 서비스에 온-프레미스 보안 정보 및 이벤트 (SIEM) 관리 시스템으로 Azure 리소스에서 toointegrate 원시 로그를 사용할 수 있습니다. 이 통합 자산에 대 한 모든 사용자, 온-프레미스 또는 클라우드에서 hello 통합 된 대시보드를 제공합니다. 그런 다음 응용 프로그램과 관련된 보안 이벤트를 집계, 상관 관계 설정, 분석 및 경고할 수 있습니다.

## <a name="is-hello-azure-log-integration-software-free"></a>Hello Azure 로그 통합 소프트웨어는 무료 입니까?
예. Azure 로그 통합 소프트웨어 hello에 대 한 무료입니다.

## <a name="where-is-azure-log-integration-available"></a>Azure 로그 통합은 어디에서 사용할 수 있나요?

현재 Azure 상용 및 Azure Government에서 사용할 수 있으며 중국 또는 독일에서는 사용할 수 없습니다.

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>Hello 저장소 계정은 Azure 로그 통합 Azure VM 로그를 가져오는 확인 하려면 어떻게 해야 합니까?
Hello 명령을 실행 **azlog 원본 목록**합니다.

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>구독 hello에서 로그는 Azure 로그 통합을 확인 하는 방법

Hello에 배치 된 감사 로그의 경우 hello **AzureResourcemanagerJson** hello 로그 파일 이름에 디렉터리 hello 구독 ID가 있습니다. Hello에 있는 로그에 대 한 해당 **AzureSecurityCenterJson** 폴더입니다. 예:

20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json

Azure Active Directory 감사 로그 hello 이름의 일부로 hello 테 넌 트 ID를 포함 합니다.

이벤트 허브에서 읽는 진단 로그는 hello 이름의 일부로 hello 구독 ID를 포함 하지 않습니다. 대신, hello 이벤트 허브 소스의 hello 만들기의 일부로 지정 된 hello 친숙 한 이름이 포함 됩니다. 

## <a name="how-can-i-update-hello-proxy-configuration"></a>Hello 프록시 구성을 업데이트 하려면 어떻게 해야 합니까?
프록시 설정 Azure 저장소 액세스를 직접 허용 하지 않는 경우 열고 hello **AZLOG 합니다. EXE 합니다. CONFIG** 파일 **c:\Program Files\Microsoft Azure 로그 통합**합니다. 업데이트 hello 파일 tooinclude hello **defaultProxy** 조직의 hello 프록시 주소를 가진 섹션. Hello 업데이트를 완료 한 후 서비스 중지 및 시작 hello hello 명령을 사용 하 여 **net stop azlog** 및 **net 시작 azlog**합니다.

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>Windows 이벤트의 hello 구독 정보를 확인 하려면 어떻게 해야 합니까?
Hello 소스를 추가 하는 동안 hello 구독 ID toohello 친숙 한 이름을 추가 합니다.

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
hello 이벤트 XML hello hello 구독 ID를 포함 하 여 메타 데이터 뒤에 있습니다.

![이벤트 XML][1]

## <a name="error-messages"></a>오류 메시지
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>Hello 명령을 실행할 때 **azlog createazureid**, 왜 hello 다음 오류가 발생?
오류:

  *실패 toocreate AAD 응용 프로그램-테 넌 트 72f988bf-86f1-41af-91ab-2d7cd011db37-이유 = '금지 됨'-메시지 = '권한이 toocomplete hello 작업이'.*

hello **azlog createazureid** 명령은 toocreate Azure 로그인 hello hello 구독에 대 한 모든 hello Azure AD 테 넌 트에 서비스 사용자에 대 한 액세스를 시도 합니다. Azure 로그인이 게스트 사용자를 해당 Azure AD 테 넌 트에만, hello 명령 실패 "권한이 toocomplete hello 작업이"입니다. Hello 테 넌 트 관리자 tooadd 요청 hello 테 넌 트에 사용자로 계정.

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>Hello 명령을 실행할 때 **azlog 권한을 부여**, 왜 hello 다음 오류가 발생?
오류:

  *역할 할당-AuthorizationFailed 만들기 경고: hello 클라이언트 janedo@microsoft.com' 개체와 id ' fe9e03e4-4dad-4328-910f-fd24a9660bd2' 권한이 없습니다. 권한 부여 tooperform 동작 'Microsoft.Authorization/roleAssignments/write' 범위에 대해 ' / 구독/70 d 95299-d689-4 c 97 b971 0d8ff0000000'.*

hello **azlog 권한을 부여** 할당 hello 판독기 toohello Azure AD 서비스 사용자의 역할을 하는 명령 (사용 하 여 만든 **azlog createazureid**) toohello 제공 된 구독입니다. Hello Azure 로그인 hello 구독 소유자 또는 공동 관리자가 아닌 경우 "권한을 부여 하지 못했습니다." 오류 메시지와 함께 실패 합니다. Azure 역할 기반 액세스 제어 (RBAC) 공동 관리자 또는 소유자의 필요한 toocomplete이이 작업은 합니다.

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>Hello 감사 로그에 hello hello 속성 정의 어디서 찾을 수 있습니까?
다음을 참조하세요.

* [Azure 리소스 관리자로 작업 감사](../azure-resource-manager/resource-group-audit.md)
* [Hello Azure 모니터 REST API에에서는 구독에 hello 관리 이벤트 나열](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>Azure Security Center 경고에 대한 세부 정보는 어디서 찾을 수 있나요?
참조 [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](../security-center/security-center-managing-and-responding-alerts.md)합니다.

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>VM 진단을 통해 수집되는 항목을 어떻게 수정할 수 있나요?
Tooget, 수정 하 고 hello Azure 진단 구성을 설정 하는 방법을 참조 [Windows를 실행 하는 가상 컴퓨터에서 PowerShell 사용 하 여 tooenable Azure 진단](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 

다음 예제는 hello hello Azure 진단 구성을 가져옵니다.

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

다음 예에서는 hello hello Azure 진단 구성을 수정 합니다. 이 구성에서 이벤트 ID 4624 및 이벤트 ID 4625 hello 보안 이벤트 로그에서 수집 됩니다. Microsoft Azure 이벤트에 대 한 맬웨어 방지 프로그램 hello 시스템 이벤트 로그에서 수집 됩니다. XPath 식 hello 사용에 대 한 자세한 내용은 참조 하십시오. [이벤트 사용](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85))합니다.

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

hello 다음 예제에서는 설정 hello Azure 진단 구성:

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

변경을 수행한 후 hello 저장소 계정 tooensure 해당 hello 올바른 이벤트를 수집할지를 확인 합니다.

Hello 설치 및 구성 중에 문제가 있는 경우을 개시 하세요는 [지원 요청](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request)합니다. 선택 **로그 통합** hello 서비스 지원을 요청 합니다.

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>Azure 로그 통합 toointegrate 네트워크 감시자 로그 내 SIEM에 사용할 수 있습니까?

Azure Network Watcher는 많은 양의 로깅 정보를 생성합니다. 이러한 로그를 SIEM 전송 업그레이드용은 toobe tooa 없습니다. 네트워크 감시자 로그에 대 한 지원만 hello 대상 저장소 계정입니다. 이러한 로그를 읽고 SIEM tooa를 사용할 수 있도록 azure 로그 통합 지원 하지 않습니다.

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
