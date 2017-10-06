---
title: "분석 데이터 보안 aaaLog | Microsoft Docs"
description: "Log Analytics에서 개인 정보를 보호하고 데이터 보안을 유지하는 방법에 대해 알아봅니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Log Analytics 데이터 보안
Microsoft는 커밋된 tooprotecting 개인 정보 데이터, 소프트웨어 및 서비스를 제공 하는 동안 유용한 정보와 hello 조직의 IT 인프라를 관리할 수 있습니다. 데이터 tooothers 맡길 때 해당 신뢰 엄격한 보안이 필요 함을 알고 합니다. Microsoft toostrict 규정 준수 및 보안 지침을 따르는-toooperating 서비스 코딩 합니다.

데이터 보안 및 보호는 Microsoft의 최우선 과제입니다. 질문, 제안 사항 또는 문제가 hello에 보안 정책을 포함 하는 정보를 다음 중 하나에 대 한 사용자 의견 [Azure 지원 옵션](http://azure.microsoft.com/support/options/)합니다.

이 문서에서는 데이터 수집, 처리 및 hello Operations Management Suite (OMS)에서 로그 분석에 의해 보안 방법을 설명 합니다. 에이전트 tooconnect toohello 웹 서비스를 사용 하거나 System Center Operations Manager toocollect 운영 데이터를 사용 하 여 로그 분석에서 사용 하기 위해 Azure 진단에서 데이터를 검색할 수 있습니다. hello 수집 데이터는 전송 hello 인터넷을 통해 Microsoft Azure에서 호스팅되는 인증서 기반 인증 및 SSL 3 toohello 로그 분석 서비스를 사용 합니다. 전송 하기 전에 hello 에이전트에서 데이터가 압축 됩니다.

hello 로그 분석 서비스 메서드를 다음 hello를 사용 하 여 클라우드 기반 데이터를 안전 하 게 관리 합니다.

* 데이터 분리
* 데이터 보존
* 물리적 보안
* 인시던트 관리
* 규정 준수
* 보안 표준 인증

## <a name="data-segregation"></a>데이터 분리
고객 데이터는 hello OMS 서비스 전체에서 각 구성 요소에 논리적으로 별도로 유지 됩니다. 모든 데이터에는 조직별로 태그가 지정됩니다. 이 태그 hello 데이터 수명 주기 동안 유지 되며 hello 서비스의 각 계층에서 적용 됩니다. 각 고객에 게 hello 장기 데이터를 저장 하는 전용된 Azure blob

## <a name="data-retention"></a>데이터 보존
인덱싱된 로그 검색 데이터가 저장 되 고 가격 계획에 따라 tooyour 유지 합니다. 자세한 내용은 [Log Analytics 가격](https://azure.microsoft.com/pricing/details/log-analytics/)을 참조하세요.

Microsoft는 hello OMS 작업 영역을 닫은 후 30 일 동안 고객 데이터를 삭제 합니다. Microsoft는 또한 hello hello 데이터가 있는 Azure 저장소 계정을 삭제 합니다. 고객 데이터가 제거될 때 물리적 드라이브는 소멸되지 않습니다.

예제에는 수집 된 데이터 유형의 hello 및 다음 표에 hello hello OMS에서 사용할 수 있는 솔루션 중 일부를 나열 합니다.

| **솔루션** | **데이터 형식** |
| --- | --- |
| 구성 평가 |구성 데이터, 메타데이터 및 상태 데이터 |
| 용량 계획 |성능 데이터 및 메타데이터 |
| 맬웨어 방지 |구성 데이터 및 메타데이터 |
| 시스템 업데이트 평가 |메타데이터 및 상태 데이터 |
| 로그 관리 |사용자 정의 이벤트 로그, Windows 이벤트 로그 및/또는 IIS 로그 |
| 변경 내용 추적 |소프트웨어 인벤토리 및 Windows 서비스 메타데이터 |
| SQL 및 Active Directory 평가 |WMI 데이터, 레지스트리 데이터, 성능 데이터 및 SQL Server 동적 관리 보기 결과 |

다음 표에서 hello 데이터 유형에 대 한 예를 보여 줍니다.

| **데이터 형식** | **필드** |
| --- | --- |
| 경고 |Alert Name, Alert Description, BaseManagedEntityId, Problem ID, IsMonitorAlert, RuleId, ResolutionState, Priority, Severity, Category, Owner, ResolvedBy, TimeRaised, TimeAdded, LastModified, LastModifiedBy, LastModifiedExceptRepeatCount, TimeResolved, TimeResolutionStateLastModified, TimeResolutionStateLastModifiedInDB, RepeatCount |
| 구성 |CustomerID, AgentID, EntityID, ManagedTypeID, ManagedTypePropertyID, CurrentValue, ChangeDate |
| 이벤트 |EventId, EventOriginalID, BaseManagedEntityInternalId, RuleId, PublisherId, PublisherName, FullNumber, Number, Category, ChannelLevel, LoggingComputer, EventData, EventParameters, TimeGenerated, TimeAdded <br>**참고:** toohello Windows 이벤트 로그에서 사용자 지정 필드가 있는 이벤트를 작성 하면 OMS에서 수집 합니다. |
| Metadata |BaseManagedEntityId, ObjectStatus, OrganizationalUnit, ActiveDirectoryObjectSid, PhysicalProcessors, NetworkName, IPAddress, ForestDNSName, NetbiosComputerName, VirtualMachineName, LastInventoryDate, HostServerNameIsVirtualMachine, IP Address, NetbiosDomainName, LogicalProcessors, DNSName, DisplayName, DomainDnsName, ActiveDirectorySite, PrincipalName, OffsetInMinuteFromGreenwichTime |
| 성능 |ObjectName, CounterName, PerfmonInstanceName, PerformanceDataId, PerformanceSourceInternalID, SampleValue, TimeSampled, TimeAdded |
| 시스템 상태 |StateChangeEventId, StateId, NewHealthState, OldHealthState, Context, TimeGenerated, TimeAdded, StateId2, BaseManagedEntityId, MonitorId, HealthState, LastModified, LastGreenAlertGenerated, DatabaseTimeModified |

## <a name="physical-security"></a>물리적 보안
로그 분석 hello OMS 서비스에는 Microsoft 담당자가 지정 되며, 및 모든 활동이 기록 되 고 감사 될 수 있습니다. hello 서비스는 Azure에서 완전히 실행 하 고 hello Azure 일반 엔지니어링 기준을 준수 합니다. Hello의 18 페이지에서 Azure 자산의 물리적 보안 hello에 대 한 세부 정보를 볼 수 있습니다 [Microsoft Azure 보안 개요](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf)합니다. 물리적으로 액세스 권한을 toosecure 영역 전송 및 종료를 포함 하는 hello OMS 서비스에 대 한 책임을 더 이상 있는 사용자 라면 누구나에 대 한 일 이내 변경 됩니다. Hello 전역 실제 인프라에서 사용 하는 방법에 대 한 읽을 수 [Microsoft 데이터 센터](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx)합니다.

## <a name="incident-management"></a>인시던트 관리
OMS에는 모든 Microsoft 서비스가 준수하는 인시던트 관리 프로세스가 있습니다. toosummarize, 여기서:

* 사용 하 여 보안 역할의 일부 tooMicrosoft 및 일부 속한 연대 모델 속한 toohello 고객
* Azure 보안 인시던트를 관리합니다
  * 인시던트를 감지하면 조사를 시작합니다.
  * Hello 영향 및 전화 사고 대응 팀 구성원이 인시던트의 심각도 평가 합니다. 증명 정보를 기반 hello 평가 표시 또는 추가 에스컬레이션 toohello 보안 대응 팀의 발생 하지 않을 수 있습니다.
  * 보안 응답 전문가 tooconduct hello 기술 또는 법정 조사 하 여 인시던트를 진단, containment, 완화 및 해결 방법 전략을 식별 합니다. Hello 보안 팀이 고객 데이터는 노출 된 tooan 불법 또는 무단에서 상태로 사용할 수 있다고 인식 하는 경우 동시에 고객 인시던트 알림 프로세스 hello의 개별, 병렬 실행을 시작 합니다.  
  * 안정화 하 고 hello 오류 로부터 복구 키를 누릅니다. hello 사고 대응 팀은 복구 계획 toomitigate hello 문제를 만듭니다. 진단과 함께 영향을 받은 시스템을 격리하는 등의 위기 억제 단계를 즉시 및 동시에 실시합니다. 긴 용어 완화 hello 즉시 위험 경과 된 후 발생 하는 계획할 수 있습니다.  
  * Hello 인시던트를 종결 하 고 사후를 수행 합니다. hello 사고 대응 팀 hello 의도 toorevise 정책, 절차 및 프로세스 tooprevent hello 이벤트의 되풀이 인시던트를 사후 hello의 hello 세부 정보에 간략하게 설명 하는 만듭니다.
* 고객에게 보안 인시던트를 알립니다.
  * 모든 가능한 표시를 세부적으로 영향을 받는 사용자에 게 영향을 받는 고객 컬렉션과 tooprovide hello 범위를 결정
  * 고객을 만들 통지 tooprovide 충분히 세부 정보가 포함 된의 끝에 한 조사를 수행 하 고 과도 하지 hello 알림 프로세스를 지연 하는 동안 tootheir 최종 사용자가 변경한 약정 수 있도록 합니다.
  * 확인 하 고 필요에 따라 hello 인시던트를 선언 합니다.
  * 불합리적인 지연 없이 법적 또는 계약적 의무에 따라 고객에게 인시턴트 공지를 전달합니다. 보안 문제에 대 한 알림 전자 메일을 통해 포함 하 여 Microsoft select 어떤 방법으로 고객의 관리자 tooone 이상 배달 됩니다.
* 팀 준비 및 교육을 실시합니다.
  * Microsoft 담당자는 필요한 toocomplete 보안 및 tooidentify 및 보안 문제가 의심 되는 보고서에 도움이 되는 인식 학습 합니다.  
  * Hello Microsoft Azure 서비스에서 작업 하는 연산자는 더하기 교육 의무 고객 데이터를 호스트 하는 액세스 toosensitive 시스템을 둘러싼 됩니다.
  * Microsoft 보안 대응 담당자는 자신의 역할에 관한 전문 교육을 받습니다.

고객 데이터 손실이 발생하는 경우 각 고객에게 1일 이내에 알립니다. 하지만 OMS에서 고객 데이터 손실이 발생한 경우는 없었습니다. 또한 Microsoft는 생성된 데이터의 복사본을 유지하며 이러한 데이터를 지리적으로 분산합니다.

Microsoft toosecurity 인시던트 응답 하는 방법에 대 한 자세한 내용은 참조 [hello 클라우드에서에서 Microsoft Azure 보안 응답](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf)합니다.

## <a name="compliance"></a>규정 준수
OMS 소프트웨어 개발 및 서비스 팀의 정보 보안 hello 및 비즈니스 요구 사항을 지원 하 고에 설명 된 대로 toolaws 및 규정을 준수 하는 거 버 넌 스 프로그램 [Microsoft Azure 보안 센터](https://azure.microsoft.com/support/trust-center/) 및 [Microsoft 보안 센터 준수](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx)합니다. 여기에는 OMS가 보안 요구 사항을 정하고 보안 컨트롤을 식별하며 위험을 관리 및 모니터링하는 방식도 설명되어 있습니다. 정책, 표준, 절차, 지침을 매년 검토합니다.

각 OMS 개발 팀원은 공식적인 애플리케이션 보안 교육을 이수합니다. 내부적으로는 소프트웨어 개발에 대한 버전 관리 시스템을 사용합니다. 각 소프트웨어 프로젝트 hello 버전 제어 시스템으로 보호 됩니다.

Microsoft에는 Microsoft의 모든 서비스를 감독 및 평가하는 보안 및 규정 준수 팀이 있습니다. 정보 보안 책임자 hello 팀을 구성 하 고 연결 되지 않은 엔지니어링 부서는 OMS 개발 hello로 합니다. hello 보안 책임자 자신의 관리 체인 있고 제품 및 서비스 tooensure 보안 및 규정 준수에 대 한 독립적인 평가 수행 합니다.

Microsoft의 이사회는 Microsoft의 모든 정보 보안 프로그램에 대한 연간 보고서를 받아 봅니다.

hello OMS 소프트웨어 개발 및 서비스 팀은 작업 중인 hello Microsoft 법률 및 규정 준수 팀 및 다른 업계 파트너 tooacquire 다양 한 인증 합니다.

## <a name="certifications-and-attestations"></a>인증 및 증명
OMS 로그 분석 hello 요구 사항을 준수를 충족 합니다.

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [결제 (PCI 규격) 카드 Industry Data Security Standard (PCI DSS)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI) hello PCI 보안 표준 위원회에서.
* [SOC(Service Organization Controls) 1 Type 1 및 SOC 2 Type 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2) 규정 준수
* HIPAA BAA(Business Associate Agreement)를 소유하는 회사에 대한 [HIPAA 및 HITECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA)
* Windows Common Engineering Criteria
* Microsoft 신뢰할 수 있는 컴퓨팅
* Azure 서비스로 OMS를 사용 하는 hello 구성 요소는 tooAzure 규정 준수 요구 사항을 준수 합니다. 자세한 내용은 [Microsoft 보안 센터 규정 준수](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx)를 참조하세요.

> [!NOTE]
> 일부 인증/증명의 경우 Log Analytics가 *Operational Insights*의 이전 이름으로 나열됩니다.
>
>


## <a name="cloud-computing-security-data-flow"></a>클라우드 컴퓨팅 보안 데이터 흐름
hello 다음 그림에 클라우드 보안 아키텍처 정보 hello 흐름으로 회사에서 하 고 궁극적으로 hello OMS 포털에서 볼 toohello 로그 분석 서비스를 이동 어떻게 보호 되는지에 그대로 합니다. 각 단계에 대 한 자세한 내용은 hello 다이어그램을 따릅니다.

![OMS 데이터 수집 및 보안 이미지](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1. Log Analytics 등록 및 데이터 수집
사용자 조직 toosend 데이터 tooLog 분석, Linux 용 OMS 에이전트 또는 Azure 가상 컴퓨터에서 실행 되는 에이전트 Windows 에이전트를 구성 합니다. Operations Manager 에이전트를 사용할 경우 구성 마법사를 사용 하 여 운영 콘솔 tooconfigure hello에에서 해당 합니다. (사용자이 문서의 독자, 다른 개별 사용자 또는 사용자 그룹) 하나 이상의 OMS 계정을 (OMS 작업 영역)을 만들고 hello 다음 계정 중 하나를 사용 하 여 에이전트를 등록 합니다.

* [조직 ID](../active-directory/sign-up-organization.md)
* [Microsoft 계정 - Outlook, Office Live, MSN](http://www.microsoft.com/account/default.aspx)

OMS 작업 영역은 데이터를 수집, 집계, 분석 및 제공하는 데 사용됩니다. 작업 영역은 주로 수단 toopartition 데이터로 사용 하며 각 작업 영역은 고유 합니다. 예를 들어 프로덕션 데이터 관리 되는 다른 작업 영역에 관리 되는 OMS 작업 영역 및 테스트 데이터 하나 toohave를 좋습니다. 작업 영역 관리자 제어 사용자 액세스 toohello 데이터를 돕습니다. 각 작업 영역에는 여러 사용자 계정이 연결될 수 있으며, 각 사용자 계정은 여러 OMS 작업 영역에 액세스할 수 있습니다. 데이터 센터 영역을 기준으로 작업 영역을 만듭니다. 각 작업 영역은 OMS 서비스 가용성에 대 한 주로 hello 지역에서 복제 된 tooother 데이터 센터입니다.

Operations Manager에 대 한 hello 구성 마법사가 완료 되 면 각 Operations Manager 관리 그룹에는 hello 로그 분석 서비스와의 연결을 설정 합니다. 그런 다음 hello 컴퓨터 추가 마법사 toochoose toosend 데이터 toohello 서비스를 수 있는 hello 관리 그룹에 컴퓨터를 사용 합니다. 다른 에이전트 형식이 각 연결 toohello OMS 서비스로 안전 하 게 합니다.

연결 된 시스템 및 hello 로그 분석 서비스 간의 모든 통신이 암호화 됩니다.  hello TLS (HTTPS) 프로토콜이 암호화에 사용 됩니다.  Microsoft SDL 프로세스 hello 뒤에 로그 분석 tooensure 암호화 프로토콜이 hello 가장 최근 발전 된 최신 상태입니다.

각 에이전트 유형은 Log Analytics에 대한 데이터를 수집합니다. hello 수집 되는 데이터 형식이 사용 되는 솔루션의 hello 형식에 따라 달라 집니다. 데이터 컬렉션에 대 한 요약을 볼 수 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다. 또한 대부분의 솔루션에 대해 자세한 컬렉션 정보를 사용할 수 있습니다. 솔루션은 미리 정의된 보기, 로그 검색 쿼리, 데이터 수집 규칙 및 처리 논리의 모음입니다. 관리자만 tooimport 로그 분석 솔루션을 사용할 수 있습니다. Hello 솔루션을 가져온 후 이동된 toohello Operations Manager 관리 서버 (사용) 하는 경우, 한 다음 선택한 tooany 에이전트 됩니다. 나중에 hello 에이전트 hello 데이터를 수집합니다.

## <a name="2-send-data-from-agents"></a>2. 에이전트에서 데이터 보내기
등록 키를 가진 모든 에이전트 형식이 등록 하 고 hello 에이전트 및 인증서 기반 인증 및 SSL 포트 443 사용 하 여 hello 로그 분석 서비스 간의 보안 연결이 설정 됩니다. OMS 보안 저장소 toogenerate를 사용 하 고 키를 유지 관리 합니다. 개인 키는 90 일 마다 회전 및 Azure에 저장 되 고 hello Azure가 관리 하는 엄격한 규정 및 규정 준수 방침 팔 로우 하는 작업입니다.

Operations Manager와 함께 hello 로그 분석 서비스와 작업 영역을 등록 하 고 hello Operations Manager 관리 서버 간의 보안 HTTPS 연결이 설정 됩니다.

Azure 가상 컴퓨터에서 실행 되는 Windows 에이전트를 읽기 전용 저장소 키는 Azure 테이블에 사용 되는 tooread 진단 이벤트입니다.

에이전트는 어떤 이유로 든 없습니다 toocommunicate toohello 서비스 hello 수집 된 데이터에에서 로컬로 저장 됩니다 임시 캐시 및 hello 관리 서버에서 tooresend hello 데이터 2 시간 동안 8 분 마다. hello 에이전트의 캐시 된 데이터는 hello 운영 체제의 자격 증명 저장소로 보호 됩니다. Hello 서비스 2 시간 후 hello 데이터를 처리할 수 없는 경우 hello 에이전트 hello 데이터 대기 됩니다. Hello 큐가 꽉 차면 OMS 성능 데이터를 시작 하는 데이터 유형에 삭제를 시작 합니다. hello 에이전트 큐 제한 레지스트리 키 이므로 필요한 경우, 수정할 수 있습니다. 수집 된 데이터는 압축 및 전송 toohello 서비스, 온-프레미스 데이터베이스는 무시 되므로 모든 부하 toothem 추가 되지 않습니다. Hello 수집한 후 전송 됩니다, 그리고 hello 캐시에서 제거 됩니다.

위에서 설명한 대로 사용자 에이전트에서 데이터는 SSL tooMicrosoft Azure 데이터 센터를 통해 전송 됩니다. 필요에 따라 hello 데이터에 대 한 express 경로 tooprovide 추가 보안을 사용할 수 있습니다. ExpressRoute 다중 프로토콜 레이블 스위칭 (MPLS) VPN, 네트워크 서비스 공급자가 제공 같은 방식으로 toodirectly 하거나 기존 WAN 네트워크에서 tooAzure 연결 되어 있습니다. 자세한 내용은 [ExpressRoute](https://azure.microsoft.com/services/expressroute/)를 참조하세요.

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3. hello 로그 분석 서비스 데이터 수신 및 처리
hello 로그 분석 서비스를 사용 하면 들어오는 데이터가 신뢰할 수 있는 원본의 인증서 및 Azure 인증을 사용 하는 hello 데이터 무결성을 확인 하 여 합니다. hello 처리 되지 않은 원시 데이터는 다음 blob으로 저장에서 [Microsoft Azure 저장소](../storage/common/storage-introduction.md) 암호화 되지 않았습니다. 그러나 각 Azure 저장소 blob에 고유 키 집합에 액세스할 수 있는 유일한 toothat 사용자 집합이 있습니다. hello 형식의 저장 된 데이터를 가져온 고 toocollect 데이터를 사용 하는 솔루션의 hello 형식에 따라 달라 집니다. 그런 다음 hello 로그 분석 서비스는 hello hello Azure 저장소 blob에 대 한 원시 데이터를 처리합니다.

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4. 로그 분석 tooaccess hello 데이터 사용
Hello 조직 계정 또는 이전에 설정 하는 Microsoft 계정을 사용 하 여 hello OMS 포털에서 tooLog 분석에에서 서명할 수 있습니다. OMS 포털 hello와 OMS의 로그 분석 간의 모든 트래픽이 보안 HTTPS 채널을 통해 전송 됩니다. Hello OMS 포털을 사용 하는 경우 세션 ID hello 사용자 클라이언트 (웹 브라우저)을 생성 하 고 hello 세션이 종료 될 때까지 데이터를 로컬 캐시에 저장 됩니다. 종료, hello 캐시가 삭제 됩니다. 개인 식별이 가능한 정보가 포함되지 않는 클라이언트 측 쿠키는 자동으로 제거되지 않습니다. 세션 쿠키는 HTTPOnly로 표시되며 보안됩니다. 미리 결정된 된 유휴 기간 후 hello OMS 포털 세션이 종료 됩니다.

Hello OMS 포털을 사용 하는 데이터 tooa CSV 파일을 내보낼 수 있습니다 및 검색 Api를 사용 하 여 데이터에 액세스할 수 있습니다. CSV 내보내기는 제한 된 too50, 내보내기 및 API 데이터 당 000 행은 제한 된 too5, 000 행 검색 수입니다.

## <a name="next-steps"></a>다음 단계
* [로그 분석 작업 시작](log-analytics-get-started.md) toolearn 로그 분석 및 분 단위로 실행할에 대 한 자세한 합니다.
