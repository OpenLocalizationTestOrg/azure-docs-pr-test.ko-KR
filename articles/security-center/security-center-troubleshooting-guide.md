---
title: "보안 센터의 문제 해결 가이드 aaaAzure | Microsoft Docs"
description: "이 문서는 Azure 보안 센터의 tootroubleshoot 문제 수 있습니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 78b3c49eb66fe3a4f80efbba3a47a87b039c07ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a>Azure 보안 센터 문제 해결 가이드
보안 센터 tootroubleshoot 관련 문제 (IT) 정보 기술 전문가, 정보 보안 분석가 및 해당 Azure 보안 센터를 사용 하는 조직과 필요한 클라우드 관리자에 대 한이 가이드는 합니다.

>[!NOTE] 
>보안 센터 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect 및 저장소 데이터를 사용 합니다. 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md) toolearn 더 합니다. 이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.
>

## <a name="troubleshooting-guide"></a>문제 해결 가이드
이 가이드는 어떻게 tootroubleshoot 보안 센터 관련 문제를 설명 합니다. 대부분 hello 보안 센터에서 수행 문제 해결의 첫 번째 hello 확인 하 여 수행 됩니다 [감사 로그](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) hello에 대 한 레코드 구성 요소 실패 했습니다. 감사 로그를 통해 다음 사항을 확인할 수 있습니다.

* 수행된 작업
* Hello 작업을 시작한 사람
* hello 작업이 발생 한 경우
* hello 작업의 hello 상태
* hello 작업을 조사 하는 데 도움이 되는 다른 속성의 hello 값

hello 감사 로그 읽기 작업 (GET)는 포함 되지 않습니다 되지만 프로그램 리소스에서 수행할 모든 쓰기 작업 (PUT, POST, DELETE)를 포함 합니다.

## <a name="microsoft-monitoring-agent"></a>Microsoft Monitoring Agent
보안 센터 hello Microsoft Monitoring Agent를 사용 하 여 –이 hello Operations Management Suite 및 Azure 가상 컴퓨터에서 보안 데이터 toocollect 로그 분석 서비스 – hello 동일한 에이전트를 사용 합니다. 데이터 수집을 활성화 한 후 hello 에이전트 hello 대상 컴퓨터에 제대로 설치 되어 실행 아래 hello 프로세스 여야 합니다.

* HealthService.exe

Hello 서비스 관리 콘솔 (services.msc)을 열면도 나타납니다 hello Microsoft Monitoring Agent 서비스가 실행 되 고 아래와 같이:

![Services](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

toosee 있는 hello 에이전트의 버전을 엽니다 **작업 관리자**, hello에 **프로세스** 탭 찾을 hello **Microsoft Monitoring Agent Service**를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다. Hello에 **세부 정보** 탭을 아래와 같이 hello 파일 버전을 확인 합니다.

![파일](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a>Microsoft Monitoring Agent 설치 시나리오
컴퓨터에 hello Microsoft Monitoring Agent를 설치 하는 경우 다른 결과 생성할 수 있는 두 가지 설치 시나리오가 있습니다. 지원 되는 hello 시나리오입니다.

* **보안 센터에서 자동으로 설치 하는 에이전트**:이 시나리오에서 위치, 보안 센터 및 로그 검색에서 수 tooview hello 경고 수 있습니다. Hello 구독 hello 리소스가 속한에 대 한 hello 보안 정책에 구성 된 전자 메일 알림을 toohello 전자 메일 주소를 받습니다.
에서도 확인할 수 있습니다.
* **Azure에 있는 VM에 수동으로 설치 된 에이전트**: 사용 중인 경우이 시나리오에서는 에이전트 다운로드 하 여 수동으로 이전 tooFebruary 2017을 설치, hello에 필터링 하는 경우에 수 tooview hello 경고 hello 보안 센터 포털에서 됩니다 구독 hello 작업 영역에 속해 있습니다. 필터 hello 구독 hello 리소스에 속한 사례를 있습니다 하지 않습니다 수 toosee 경고 합니다. 에 속한 hello 구독 hello 작업 영역에 대 한 hello 보안 정책에 구성 된 전자 메일 알림을 toohello 전자 메일 주소를 받습니다.

>[!NOTE]
> 둘째, tooavoid hello 동작 hello에 설명 된 hello hello 에이전트의 최신 버전 다운로드 있는지 확인 합니다.
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a>모니터링 에이전트 네트워크 요구 사항 문제 해결
보안 센터와 tooconnect tooand 레지스터 에이전트에 대 한 hello 포트 번호 및 도메인 Url을 포함 하 여 toonetwork 리소스에 액세스 가져야 합니다.

- 프록시 서버에 대 한 적절 한 프록시 서버를 에이전트 설정에 구성 된 리소스가 hello tooensure를 해야 합니다. 에 자세한 내용은이 문서를 읽기 [어떻게 toochange hello 프록시 설정](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings)합니다.
- 인터넷 액세스 toohello 제한 하는 방화벽, tooconfigure 사용자 방화벽 toopermit 액세스 tooOMS이 필요 합니다. 에이전트 설정에서 아무 작업도 필요하지 않습니다.

다음 표에서 hello 통신에 필요한 리소스를 보여 줍니다.

| 에이전트 리소스 | 포트 | HTTPS 검사 무시 |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | 예 |
| *.oms.opinsights.azure.com | 443 | 예 |
| *.blob.core.windows.net | 443 | 예 |
| *.azure-automation.net | 443 | 예 |

Hello 에이전트 온 보 딩 문제를 발생 하는 경우 확인 되었는지 tooread hello 문서 [tootroubleshoot Operations Management Suite 온 보 딩 문제 어떻게](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues)합니다.


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a>제대로 작동하지 않는 끝점 보호 문제 해결

hello 게스트 에이전트는 모든 항목의 부모 프로세스 hello hello [Microsoft 맬웨어 방지](../security/azure-security-antimalware.md) 확장 않습니다. Hello 게스트 에이전트 프로세스가 실패 하면 hello hello 게스트 에이전트의 자식 프로세스로 실행 되는 Microsoft 맬웨어 방지 실패할 수 있습니다.  과 같은 경우에는 권장된 tooverify hello 다음 옵션:

- Hello 대상 VM 사용자 지정 이미지 고 hello 작성자의 hello VM 게스트 에이전트를 설치 하지 합니다.
- Hello 대상 Windows VM의 다음 Linux VM의 hello 맬웨어 방지 확장의 hello Windows 버전을 설치 하는 대신 Linux VM이 실패 합니다. hello Linux 게스트 에이전트 요구 사항도 OS 버전 및 필요한 패키지 있으며 이러한 요구 사항을 충족 되지 않으면 hello VM 에이전트가 작동 하지 않습니다 발생 하거나 합니다. 
- 경우 hello VM 게스트 에이전트의 이전 버전으로 만들어졌습니다. 에 있는 경우에 오래 된 일부 에이전트 수 하지 자동 업데이트 자체 toohello 최신 버전 하며 toothis 문제가 발생할 수 있어야 합니다. 사용자 고유의 이미지를 만드는 경우 항상 최신 버전의 게스트 에이전트 hello를 사용 합니다.
- 일부 공급 업체 관리 소프트웨어는 hello 게스트 에이전트를 사용 하지 않도록 설정 하거나 액세스 toocertain 파일 위치를 차단할 수 있습니다. 제 3 자 VM에 설치 되어 있는 경우 hello 제외 목록에 해당 hello 에이전트 인지 확인 합니다.
- 특정 방화벽 설정 또는 보안 그룹 NSG (네트워크) 게스트 에이전트에서 네트워크 트래픽을 tooand를 차단할 수 있습니다.
- 특정 ACL(액세스 제어 목록)에서 디스크 액세스를 차단할 수 있습니다.
- 디스크 공간 부족 hello 게스트 에이전트는 제대로 작동을 차단할 수 있습니다. 

Microsoft 맬웨어 방지 사용자 인터페이스를 사용 하지 않도록 설정 하는 기본 hello,으로 읽기 [Azure 리소스 관리자 Vm 배포 후에 Microsoft 맬웨어 방지 프로그램 사용자 인터페이스를 사용 하도록 설정](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) 방법에 대 한 자세한 내용은 tooenable 필요한 경우.

## <a name="troubleshooting-problems-loading-hello-dashboard"></a>Hello 대시보드를 로드 하는 문제 해결

을 hello 보안 센터 대시보드를 로드 하는 문제가 발생 하는 경우 확인 hello 구독 tooSecurity 센터 (예: hello 첫 번째 사용자 hello 구독을 사용 하 여 보안 센터를 열 하나)을 등록 하는 해당 hello 사용자와 hello 사용자에 tooturn 려가 데이터 수집이 *소유자* 또는 *참가자* hello 가입 합니다. 에 있는 사용자도이 순간부터 *판독기* hello 구독 hello 대시보드/경고/권장 구성/정책 볼 수 있습니다.

## <a name="contacting-microsoft-support"></a>Microsoft 지원에 문의
이 문서에서 제공 하는 hello 지침을 사용 하 여 몇 가지 문제를 식별할 수 있습니다, 찾을 수 있습니다 다른 hello 보안 센터 공용의 설명 대로 [포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter)합니다. 그러나 추가로 문제 해결이 필요한 경우 아래와 같이 **Azure Portal**을 사용하여 새로운 지원 요청을 열 수 있습니다. 

![Microsoft 지원](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a>참고 항목
이 문서에서는 방법에 대해 배웠습니다 Azure 보안 센터에서 tooconfigure 보안 정책입니다. Azure 보안 센터에 대해 자세히 toolearn hello 다음을 참조 합니다.

* [Azure 보안 센터 계획 및 운영 가이드](security-center-planning-and-operations-guide.md) -학습 방법을 tooplan hello 디자인 고려 사항 tooadopt Azure 보안 센터를 이해 하 고 있습니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) — Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.

