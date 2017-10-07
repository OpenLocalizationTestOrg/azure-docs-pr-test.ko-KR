---
title: "클라우드 서비스 역할 재활용 aaaCommon 원인은 | Microsoft Docs"
description: "재활용이 중요한 가동 중지 시간을 갑작스럽게 발생시킬 수 있는 클라우드 서비스 역할입니다. 다음은 가동 중지 시간 감소 하는 데 수 있는 역할 toobe 재활용 발생 하는 몇 가지 일반적인 문제입니다."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>역할 toorecycle 발생 하는 일반적인 문제
이 문서는 hello 배포 문제의 일반적인 원인 중 일부에 대해 설명 하 고 toohelp 문제 해결 정보를 제공 합니다. 이러한 문제를 해결 합니다. 응용 프로그램에 문제가 있음을 나타내는 때 hello 역할 인스턴스가 toostart, 실패 또는 hello 초기화, 사용 중 및 중지 중 상태 사이 순환 합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>런타임 종속성 누락
응용 프로그램에서 역할의 hello 포함 되지 않은 모든 어셈블리에 의존 하는 경우.NET Framework 또는 hello Azure 관리 되는 라이브러리, hello 응용 프로그램 패키지에 해당 어셈블리를 명시적으로 포함 해야 합니다. 기타 Microsoft 프레임워크가 기본적으로 Azure에서 사용할 수 없다는 사실을 염두에 두십시오. 역할이 이러한 프레임 워크를 사용 하는 경우에 해당 어셈블리 toohello 응용 프로그램 패키지를 추가 해야 합니다.

응용 프로그램 패키지를 작성 하기 전에 hello 다음을 확인 합니다.

* Visual studio를 사용 하는 경우 확인 있는지 hello **로컬 복사** 너무 속성이**True** 참조 된 어셈블리의 hello Azure SDK는 포함 되지 않은 프로젝트에 각 설정 또는.NET Framework hello에 대 한 합니다.
* Hello web.config 파일 hello 컴파일 요소에 사용 되지 않는 모든 어셈블리를 참조 하지 않는지 확인 합니다.
* hello **빌드 작업** 파일이 너무 설정의 각.cshtml**콘텐츠**합니다. 이렇게 하면 hello 파일 hello 패키지에 올바르게 표시 되며 다른 참조 된 파일 tooappear hello 패키지에 있습니다.

## <a name="assembly-targets-wrong-platform"></a>어셈블리가 잘못된 플랫폼을 목표로 합니다.
Azure는 64비트 환경입니다. 따라서 32비트 대상에 컴파일된 .NET 어셈블리는 Azure에서 작동하지 않습니다.

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>초기화하거나 중지하는 동안 처리되지 않은 예외를 throw하는 역할
Hello의 hello 메서드에서 throw 되는 모든 예외 [RoleEntryPoint] hello를 포함 하는 클래스 [OnStart], [OnStop], 및 [실행]메서드는 처리 되지 않은 예외입니다. 이러한 메서드 중 하나에서 처리 되지 않은 예외가 발생 하는 경우에 hello 역할이 재활용 됩니다. Hello 역할은 반복적으로 재활용 하는 경우 toostart 시도할 때마다 처리 되지 않은 예외가 throw 할 수 있습니다.

## <a name="role-returns-from-run-method"></a>역할은 실행 메서드에서 반환합니다.
hello [실행] 메서드를 의도 한 toorun 무기한으로 합니다. Hello를 재정의 하는 코드 경우 [실행] 메서드를 것 무한 대기 상태가 됩니다. 경우 hello [실행] hello 역할이 재활용 메서드가 반환 합니다.

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>잘못된 DiagnosticsConnectionString 설정
서비스 구성 파일 hello를 지정 해야 Azure 진단을 사용 하는 응용 프로그램 `DiagnosticsConnectionString` 구성 설정입니다. 이 설정은 Azure에서 HTTPS 연결 tooyour 저장소 계정을 지정 해야 합니다.

tooensure 하 여 `DiagnosticsConnectionString` 응용 프로그램 패키지 tooAzure를 배포 하기 전에 설정이 올바른지, hello 다음을 확인 합니다.  

* hello `DiagnosticsConnectionString` 지점을 tooa 유효한 저장소 계정을 Azure에서 설정 합니다.  
  기본적으로이 설정은 가리키므로 toohello 에뮬레이트된 저장소 계정에 응용 프로그램 패키지를 배포 하기 전에이 설정을 명시적으로 변경 해야 합니다. 이 설정을 변경 하지 않는 경우 hello 역할 인스턴스 toostart hello에 대 한 진단 모니터를 시도할 때 예외가 throw 됩니다. 이 역할 인스턴스 toorecycle hello 무기한으로 인해 수 있습니다.
* hello 연결 문자열에에서 지정 된 hello 다음 [형식](../storage/common/storage-configure-connection-string.md)합니다. (hello 프로토콜 HTTPS로 지정 되어야 합니다.) 대체 *MyAccountName* hello 저장소 계정의 이름으로 및 *MyAccountKey* 자신의 액세스 키로:    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  Microsoft Visual Studio 용 Azure 도구를 사용 하 여 응용 프로그램을 개발 하는 경우이 값 속성 페이지 tooset hello를 사용할 수 있습니다.

## <a name="exported-certificate-does-not-include-private-key"></a>내보낸 인증서는 개인 키를 포함하지 않습니다.
toorun SSL에서 웹 역할을 확인 해야 내보낸된 관리 인증서 hello 개인 키를 포함 합니다. Hello를 사용 하는 경우 *Windows 인증서 관리자* tooexport hello 인증서 수 있는지 tooselect **예** hello에 대 한 **hello 개인 키 내보내기** 옵션입니다. hello 인증서는 hello 현재 지원 되는 유일한 형식 hello PFX 형식으로 내보내야 합니다.

## <a name="next-steps"></a>다음 단계
클라우드 서비스에 대한 [문제해결 문서](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.

[Kevin Williamson의 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)에서 더 많은 역할 재활용 시나리오를 보세요.

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[실행]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
