---
title: "Azure 보고 도구를 사용 하 여 개인 데이터의 aaaDocument 보호 | Microsoft Docs"
description: "어떻게 toouse 보고 Azure 서비스 및 기술 toohelp 개인 데이터의 개인 정보를 보호 합니다."
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>Azure 보고 도구로 개인 데이터의 문서 보호

이 문서에서는 Azure reporting toouse 서비스 하는 방법을 설명 하 고 기술 toohelp 개인 데이터의 개인 정보를 보호 합니다.

## <a name="scenario"></a>시나리오

Hello 미국에서 본사는 큰 크루즈 회사 hello 지중해, Adriatic, 발트어 바다 뿐 아니라 hello 영국 제도에서 해당 작업 toooffer 여정이 확장 합니다. toohelp 이탈리아를 더 작은 여러 크루즈 줄 획득 이러한 노력을이 통해 독일, 덴마크 및 hello 영국

hello 회사에서 회사 데이터의 처리 및 저장에 대 한 Microsoft Azure를 사용 합니다. 여기에는 전 세계 고객 기반의 이름, 주소, 전화 번호 및 신용 카드 정보와 같이 식별 가능한 개인 정보가 포함됩니다. 또한 모든 위치에 주소, 전화 번호, 세금 id 번호, 회사 직원에 대 한 의료 보험 정보 등 기존의 인적 자원 정보를 포함 합니다. hello 크루즈 줄에는 현재 및 과거 고객과 개인 정보 tootrack 관계를 포함 하는 보상 및 충성도 프로그램 멤버의 큰 데이터베이스 유지 관리 합니다.

회사 직원 hello 네트워크 hello 회사의 원격 사무실 및 여행사에서 액세스 하는 hello world 주변에 있는 toosome 회사 리소스에 액세스 했습니다.

## <a name="problem-statement"></a>문제 설명

hello 회사 직원의 및 고객의 개인 데이터를 통해 Azure 관리 및 보안 기능 tooimpose 개인 데이터 액세스 tooand 처리에 엄격한 제어를 사용 하 고 있어야 하는 다중 계층된 보안 전략의 hello 개인 정보를 보호 해야 합니다. 수 toodemonstrate toointernal 및 외부 감사자의 보호를 측정 합니다.

## <a name="company-goal"></a>회사 목표

해당 방어 보안 전략의 일환으로, 회사 목표 tootrack 개인 데이터의 모든 액세스 tooand 처리 되며 설명서 개인 데이터에 대 한 적절 한 개인 정보 보호의 위치와 작업에 있는지 확인 하세요.

## <a name="solutions"></a>솔루션

Microsoft Azure에서는 포괄적인 모니터링, 로깅 및 진단 도구 toohelp 추적 및 활동과 액세스 하 고 개인 데이터, 데이터 및 제 3 자 액세스 toopersonal 데이터의 흐름을 지리적 처리와 관련 된 이벤트를 기록 합니다. Hello 클라우드에서 개인 데이터의 보안 공유 책임 이기 때문에 Microsoft 고객에 게 제공 됩니다.

- 고객 데이터의 자체적인 처리에 대한 자세한 정보

- Microsoft에서 관리하는 보안 조치

- 고객의 데이터를 보낼 위치와 방법

- Microsoft의 개인 정보 검토 프로세스의 세부 정보

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)는 Microsoft의 클라우드 기반, 다중 테넌트 디렉터리 및 ID 관리 서비스입니다. 서비스의 로그인 hello 및 감사 보고 기능 자세한 로그인 및 응용 프로그램 사용 현황 활동 정보 toohelp 모니터링 하 고 적절 한 액세스 toocustomers 및 직원의 개인 데이터 확인을 제공 합니다.

활동 보고서에는 다음 두 가지 유형이 있습니다.

- hello [활동 보고서/로그 감사](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) 시스템 활동/작업의 세부 레코드를 제공 합니다.

- hello [로그인 활동 보고서/로그](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) hello 감사 보고서에 나열 된 각 활동을 수행한 사용자 표시

Hello 두를 함께 사용 hello 수행 하는 각 작업의 기록과 각각을 수행한 사용자를 추적할 수 있습니다. 두 보고서 유형 모두 사용자 지정이 가능하고 필터링할 수 있습니다.

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>액세스 하려면 어떻게 합니까 hello 감사 및 보안 로그?

hello 감사 및 보안 로그에에서 액세스할 수 있습니다 hello Active Directory 포털에서 세 가지 방법으로: hello를 통해 **활동** 섹션 (중 하나를 선택 **감사 로그** 또는 **로그인**), 또는 **사용자 및 그룹** 또는 **엔터프라이즈 응용 프로그램** 아래 **관리** Active Directory에 있습니다. 또한 hello Azure Active Directory를 통해 보고서에 액세스할 수 API를 보고 합니다. 

1. Hello Azure 포털에서에서 선택 **Azure Active Directory 합니다.**

2. Hello에 **활동** 섹션에서 **감사 로그 합니다.**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. Hello 목록 보기를 클릭 하 여 사용자 지정 **열** hello 도구 모음에서입니다.

4.  항목에 대 한 모든 사용 가능한 세부 정보 목록 보기 toosee hello에서에서 항목을 선택 합니다.

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

또한 Azure Active Directory 보고에는 **위험 플래그가 지정된 사용자** 및 **위험한 로그인**이라는 두 가지 유형의 보안 보고서가 포함되어 Azure 환경에서 잠재적인 위험을 모니터링하는 데 도움이 될 수 있습니다.

보고 서비스는 hello에 대 한 자세한 내용은 참조 하십시오. [Azure Active Directory 보고](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

방문 [Azure Active Directory 작업 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) Azure Active Directory에서 사용할 수 있는 hello 보고서에 대 한 자세한 내용은 합니다. 이 사이트에 방법에 대 한 자세한 내용은 tooaccess 사용 하 여 [감사 로그를 작업 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) 및 [로그인 활동 보고서](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) hello 포털에서입니다. 또한 [위험에 대한 플래그가 지정된 사용자](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) 및 [위험한 로그인](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins) 보안 보고서에 대한 정보도 포함됩니다.

Hello 방문 [Azure Active Directory 감사 API 참조](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) 방법에 대 한 자세한 내용은 사이트 tooconnect tooAzure 디렉터리 프로그래밍 방식으로 보고 합니다.

### <a name="log-analytics"></a>Log Analytics

[로그 분석](https://azure.microsoft.com/services/log-analytics/) 수 [Azure 모니터에서 데이터를 수집](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate 다른 데이터와 분석 추가 기능을 제공 합니다. Azure Monitor는 Azure 환경에 대한 모니터링 데이터를 수집하고 분석합니다. 

로그 검색, 뷰 및 솔루션과 같은 Log Analytics의 분석 도구는 전체 사용자 환경의 중앙 집중식 분석을 제공하는 모든 수집된 데이터에 대해 작동합니다. 로그 분석 집계 하 고 Windows 이벤트 로그, IIS 로그 및 toounauthorized 사용자 개인 데이터에 노출 시킬 수 있는 잠재적인 개인 데이터 위반을 감지 하는 데 도움이 되는 Syslogs 분석할 수 있습니다.

#### <a name="how-do-i-use-log-analytics"></a>Log Analytics를 사용하려면 어떻게 할까요?

로그 분석 hello OMS 포털 또는 hello 모든 웹 브라우저에서 Azure 포털을 통해 액세스할 수 있습니다. 로그 분석 쿼리 언어 tooquickly 검색을 포함 하며 hello 리포지토리에 데이터를 통합 합니다. 만들 하 고 로그 검색 toodirectly 저장 hello 포털에서 데이터를 분석할 수 있습니다.

toocreate hello Azure 포털에서에서 로그 분석 작업 영역 다음 hello지 않습니다.

1. 선택 **로그 분석** hello hello Marketplace의에서 서비스 목록에서 합니다.

2. 선택 **만들기,** 다음 hello OMS 작업 영역 이름을 지정 구독, 리소스 그룹, 위치를 선택 하 고 가격 책정 계층입니다.

3. 클릭 **확인** toodisplay 작업 영역 목록이 있습니다.

4. 작업 영역 toosee 세부 정보를 선택 합니다.

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

Hello 방문 [로그 분석 설명서](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn hello 서비스에 대 한 자세한 합니다.

Hello 방문 [로그 분석 작업 영역 시작](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) 자습서 toocreate는 평가 작업 영역 어떻게 toouse hello 서비스의 hello 기본 사항 학습 및 합니다.

보다 구체적인 정보에 대 한 웹 페이지에 나오는 tooconnect toouse 로그 분석 hello로 기록 하는 방법에 hello를 방문 하 고 위에 설명 된 키를 누릅니다.

[Log Analytics의 Windows 이벤트 로그 데이터 원본](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[Log Analytics의 IIS 로그](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[Log Analytics의 Syslog 데이터 원본](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Azure Monitor/Azure 활동 로그 

[Azure Monitor](https://azure.microsoft.com/services/monitor/)는 대부분의 Microsoft Azure 서비스에 대한 기본 수준의 인프라 메트릭과 로그를 제공합니다.
모니터링 toogain Azure 응용 프로그램에 대 한 깊은 통찰력 제공 합니다. Azure 모니터는 hello Azure 진단 확장 (Windows 또는 Linux) 대부분의 응용 프로그램 수준 메트릭 및 로그를 수집 하려면 사용 합니다. [Azure 활동 로그 hello](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) Azure 모니터를 볼 수는 hello 리소스 중 하나입니다. 모든 API 호출을 추적하고 [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)에서 발생하는 활동에 대한 다양한 정보를 제공합니다.
Hello Azure 인프라와 같이 리소스에 대 한 자세한 내용은 hello (이전에 운영 또는 감사 로그 호출) 활동 로그를 검색할 수 있습니다. 

Hello 정보의 대부분 기록 하지만 hello 활동 로그 tooperformance과 서비스 상태를 관련 된., 정보를 데이터의 관련된 tooprotection 이기도 합니다. Hello 활동 로그를 사용 하 여 hello 확인할 수 있습니다 "부분, who, 시기 및" 모든 쓰기 작업 (PUT, POST, DELETE) Azure 구독에서 hello 리소스에 대해 수행에 대 한 합니다.

예를 들어 관리자가 개인 데이터의 hello 보호에 영향을 줄 수 있는 네트워크 보안 그룹을 삭제 레코드를 제공 합니다. 활동 로그 항목은 Azure Monitor에 90일 동안 저장됩니다.

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>Azure 모니터에 의해 수집 된 hello 데이터를 사용 하려면 어떻게 해야 합니까?

다양 한 방법으로 toouse hello 데이터 hello 활동 로그에 및 기타 Azure 모니터 리소스.

- Hello 데이터 tooother 위치 실제 줄에서 스트리밍할 수 있습니다.

- 사용 하 여 hello 기본값 보다 더 긴 기간에 대 한 hello 데이터를 저장할 수 있습니다는 [Azure 저장소 계정](https://docs.microsoft.com/azure/storage/common/storage-introduction) 및 보존 정책을 설정 합니다.

- Hello를 사용 하 여 그래픽 및 차트를 보고서의 데이터를 시각적 hello 수 [Azure 포털](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), 또는 제 3 자 시각화 도구입니다.

- Hello CLI 명령 Azure 모니터 REST API를 사용 하 여 hello 데이터를 쿼리할 수 [PowerShell](https://docs.microsoft.com/powershell/) cmdlet 또는.NET SDK를 환영 합니다.

Azure 모니터 시작 tooget 선택 **더 서비스** hello Azure 포털의에서.

1. 너무 아래로 스크롤하여**모니터** hello에 **모니터링 및 관리** 섹션.

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  Hello에서 모니터 열립니다 **활동 로그** 보기.

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

수 만들고 저장 pin hello 가장 중요 한 쿼리 tooa 포털 대시보드에서 한 공통 필터 다음에 대 한 쿼리 조건을 충족 하는 이벤트가 발생 한 경우 항상 변경할 수 있습니다.

1. 리소스 그룹, timespan 및 이벤트 범주에 따라 hello 보기를 필터링 할 수 있습니다.

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. Hello를 클릭 하 여 다음 쿼리 tooa 포털 대시보드에 고정할 수 있습니다 **Pin** 단추입니다. 이렇게 하면 서비스에 대한 운영 데이터 정보를 제공하는 단일 출처를 만들 수 있습니다. hello 대시보드에서 hello 쿼리 이름 및 결과 수가 표시 됩니다.

모든 Azure 리소스에 대 한 hello 모니터 tooview 메트릭을 사용 하 여 하 고 진단 설정 및 경고를 구성 다음 hello 로그를 검색할 수도 있습니다. Toouse hello Azure 모니터 및 작업 로그를 참조 하는 방법에 대 한 자세한 내용은 [Azure 모니터를 시작](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started)합니다.

### <a name="azure-diagnostics"></a>Azure 진단 

Azure의 hello 진단 기능을 사용 하면 여러 원본에서 데이터의 컬렉션입니다. hello 보안 로그를 포함 하는 hello Windows 이벤트 로그, 추적 및 개인 데이터의 보호를 문서화에 특히 유용할 수 있습니다. hello 보안 로그 권한 변경, 특정 유형의 공격, 보안 관련 정책 변경, 보안 그룹 구성원 변경 등에 나타내는 패턴 검색 뿐 아니라 로그온 성공 및 실패 이벤트를 추적 합니다.

예를 들어 이벤트 ID 4695 감사 가능한 보호 된 데이터의 있습니다 시도 toohello unprotection을 경고합니다. 이 적용 toohello API DPAPI (데이터 보호), 개인 키, 저장 된 자격 증명 및 기타 기밀 정보 같은 tooprotect 데이터 하는 데 도움이 됩니다.

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>Windows Vm에 대 한 hello 진단 확장 하려면 어떻게 해야 합니까?

Windows VM에 대 한 PowerShell tooenable hello 진단 확장을 따라서 toocollect 로그 데이터도 사용할 수 있습니다. 이렇게 hello 단계 (리소스 관리자 또는 클래식)를 사용 하는 배포 모델에 따라 다릅니다. hello 리소스 관리자 배포 모델을 통해 생성 된 기존 VM에 tooenable hello 진단 확장을 hello를 사용할 수 있습니다 [집합 AzureRMVMDiagnosticsExtension PowerShell cmdlet](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1)합니다.

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* hello 진단 구성을 XML에 포함 된 hello 경로 toohello 파일이 있습니다. VM에 Azure 진단 사용에 대 한 지침 보다 자세한 참조 [Windows를 실행 하는 가상 컴퓨터에서 PowerShell 사용 하 여 tooenable Azure 진단 합니다.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

hello Azure 진단 확장 hello 수집 된 데이터 tooan Azure 저장소 계정에 전송 하거나 Application Insights와 같은 tooservices 보낼 수 있습니다. 그런 다음 감사에 대 한 hello 데이터를 사용할 수 있습니다.

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>진단 데이터를 저장하고 보려면 어떻게 하나요?

것이 중요 한 tooremember 오류 진단 데이터가 toohello Microsoft Azure 저장소 에뮬레이터 또는 tooAzure 저장소 전송 하지 않을 경우 영구적으로 저장 되지 않습니다. Azure 저장소에 진단 데이터 toostore 및 보기는 다음이 단계를 따르십시오.

1. Hello ServiceConfiguration.cscfg 파일에 저장소 계정을 지정 합니다. Azure 진단 hello Blob 서비스 또는 데이터의 hello 유형에 따라 hello 테이블 서비스에 사용할 수 있습니다. Windows 이벤트 로그는 테이블 형식으로 저장됩니다.

2. Hello 데이터를 전송 합니다. Hello 구성 파일을 통해 tootransfer hello에 대 한 진단 데이터를 요청할 수 있습니다. 에 대 한 SDK 2.4 및 이전 프로그래밍 방식으로 hello 요청을 만들 수도 있습니다.

3. Hello 데이터를 사용 하 여 볼 [Azure 저장소 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [서버 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) Visual Studio에서 또는 [Azure 진단 관리자](https://www.cerebrata.com/products/azure-diagnostics-manager) Azure Management Studio에서.

방법에 대 한 자세한 내용은 각 tooperform 이러한 단계의 참조 [Azure 저장소에 진단 데이터 저장 및 확인 합니다.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Azure Storage 분석 

Storage Analytics는 성공 및 실패 한 요청 tooa 저장소 서비스에 대 한 세부 정보를 기록 합니다. 이 정보는 hello 서비스에 저장 된 액세스 toopersonal 데이터 문서화에 도움이 될 수 있는 사용된 toomonitor 개별 요청을 수 있습니다. 하지만 저장소 분석 로깅은 저장소 계정에 대해 기본적으로 사용하지 않도록 설정됩니다. Hello Azure 포털에서에서 설정할 수 있습니다.

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>저장소 계정에 대한 모니터링은 어떻게 구성하나요?

저장소 계정에 대 한 모니터링 tooconfigure 다음 hello지 않습니다.

1. 선택 **저장소 계정은** hello Azure 포털에서에서 다음 계정의 hello toomonitor hello 이름을 선택 합니다.

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. Hello에 **모니터링** 섹션에서 **진단 합니다.**

3.  선택 hello **형식** 메트릭 데이터의 각 서비스 (Blob, 테이블, 파일)에 대 한 toomonitor 원하는 합니다. tooinstruct Azure 저장소 toosave 진단 로그에 대 한 읽기, 쓰기 및 삭제 요청을 hello blob, 테이블 및 큐 서비스 선택에 대 한 **로그 Blob, 테이블 로그** 및 **로그 큐에 대기 합니다.**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. Hello hello 슬라이더를 사용 하 여 hello 맨 아래에, 설정 **보존** 정책 일 (1-365 값). 7 일 hello 기본값입니다.

5. 선택 **저장** tooapply hello 구성 설정입니다.

저장소 로깅 로그 항목 hello 다음 개별 요청에 대 한 정보를 포함 합니다.

- 시작 시간, 종단 간 대기 시간, 서버 대기 시간 등의 타이밍 정보입니다.

- Hello 연산 유형 같은 hello 저장소 작업의 세부 정보를 액세스, 성공 또는 실패 및 hello HTTP 상태 코드 반환 toohello 클라이언트 hello 저장소 개체 hello 클라이언트의 hello 키는 됩니다.

- 사용 되는 인증 hello 클라이언트 hello 유형의 같은 인증 세부 정보입니다.

- Hello ETag 값과 마지막으로 수정 된 타임 스탬프와 같은 동시성 정보입니다.

- hello 요청 및 응답 메시지의 hello 크기입니다.

자세한 방법은 tooenable 저장소 분석 로깅, 참조 [hello Azure 포털에서에서 저장소 계정을 모니터링 합니다.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Azure 보안 센터 

[Azure 보안 센터](https://azure.microsoft.com/services/security-center/) 모니터 순서 tooprevent에 Azure 리소스가의 보안 상태 hello 및 위협, 검색 및 응답에 대 한 권장 사항을 제공 합니다. 여러 가지 방법으로 toohelp 문서 hello 개인 정보 개인 데이터를 보호 하는 보안 조치를 제공 합니다.

보안 상태 모니터링을 통해 보안 정책 준수를 보장할 수 있습니다. 보안 모니터링 하는 것은 조직의 표준 또는 모범 사례를 충족 하지 않는 리소스 tooidentify 시스템을 감사 하는 사전 전략입니다. 다음 리소스는 hello hello 보안 상태를 모니터링할 수 있습니다.

- Compute(가상 컴퓨터 및 클라우드 서비스)

- 네트워킹(가상 네트워크)

- 저장소 및 데이터(서버와 데이터베이스 감사 및 위협 감지, TDE, 저장소 암호화)

- 응용 프로그램(잠재적 보안 문제)

이러한 범주에 대 한 보안 문제 개인 데이터의 위협 toohello 개인 정보 보호를 따를 수 있습니다.

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>내 Azure 리소스의 hello 보안 상태를 보려면 어떻게 해야 합니까?

보안 센터 리소스를 Azure의 hello 보안 상태를 정기적으로 분석합니다. Hello에서 식별 하는 잠재적인 보안 취약점을 볼 수 있습니다 **방지** hello 대시보드의 섹션.

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. Hello에 **방지** 섹션을 선택 하는 hello **계산** 바둑판식으로 배열입니다. 여기에 표시 됩니다는 **개요,** hello 함께 **가상 컴퓨터** 모든 Vm 및의 보안 상태를 나열 하 고 hello **클라우드 서비스** 웹 및 작업자 역할의 목록 보안 센터에 의해 모니터링 됩니다.

2. Hello에 **개요** 탭, 자세한 내용은 추천 tooview에 두 번째입니다.

3. Hello에 **가상 컴퓨터** 탭 VM tooview 추가 세부 정보를 선택 합니다.

Azure 보안 센터에서 데이터 수집을 활성화 하는 경우 Microsoft Monitoring Agent hello 자동으로 모든 기존에 프로 비전 하 고 새로 지원 되는 모든 배포 된 가상 컴퓨터. 이 에이전트에서 수집된 데이터는 구독 또는 새 작업 영역에 연결된 기존 [Log Analytics](https://azure.microsoft.com/services/log-analytics/) 작업 영역 중 하나에 저장됩니다.

[위협 인텔리전스 보고서](https://docs.microsoft.com/azure/security-center/security-center-threat-report)는 Security Center에서 제공됩니다. 이러한 toohelp hello 공격자의 id, 목표, 현재 및 기록 공격 캠페인 및 전술을, 도구 및 사용 되는 프로시저를 식별 유용한 정보를 제공 합니다. 마이그레이션 및 수정 정보도 포함됩니다.

이러한 위협 보고서의 주요 목적은 hello은 toohelp 있습니다 toorespond 효과적으로 toohello 즉시 위협 요소 및 도움말 take 측정 이후에 toomitigate hello 문제입니다. 프로그램 사고 대응 보고 및 감사용으로 문서화 하는 경우에 hello 보고서의 hello 정보 유용할 수 있습니다.

hello 위협 인텔리전스 보고서가 표시 됩니다. Hello에 대 한 링크를 통해 액세스 하는 PDF 형식으로 **보고서** hello 필드 **실행 된 의심 스러운 프로세스** Azure 보안 센터에서 각 보안 경고 블레이드입니다.

방법을 사용 하 여 tooview hello 위협 인텔리전스 보고서에 대 한 자세한 내용은 참조 하십시오. [Azure 보안 센터 위협 인텔리전스 보고서입니다.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>다음 단계:

[Azure Active Directory 보고 API hello 시작](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[Log Analytics란?](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Microsoft Azure의 모니터링 개요](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[소개 toohello Azure 활동 로그 (비디오)](https://azure.microsoft.com/resources/videos/intro-activity-log/)
