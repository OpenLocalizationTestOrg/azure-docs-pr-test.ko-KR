---
title: "보안 센터 데이터 보안 aaaAzure | Microsoft Docs"
description: "이 문서에서는 Azure 보안 센터에서 데이터 관리하고 보호하는 방법을 설명합니다."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 30f8b11272dc5df6d485608abdaa62ba57e63f23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-data-security"></a>Azure 보안 센터 데이터 보안
toohelp 고객 방지 감지 하 고 toothreats 응답, Azure 보안 센터를 수집 하 고 구성 정보, 메타 데이터, 이벤트 로그, 크래시 덤프 파일 등의 보안 관련 데이터를 처리 합니다. Microsoft toostrict 규정 준수 및 보안 지침을 따르는-toooperating 서비스 코딩 합니다.

이 문서에서는 Azure 보안 센터에서 데이터 관리하고 보호하는 방법을 설명합니다.

>[!NOTE] 
>보안 센터는 초기 년 6 월 2017 년 부터는 hello Microsoft Monitoring Agent toocollect를 사용 하 고 데이터를 저장 합니다. 참조 [Azure 보안 센터 플랫폼 마이그레이션](security-center-platform-migration.md) toolearn 더 합니다. 이 문서의 정보 hello 전환 toohello Microsoft Monitoring Agent 후 보안 센터 기능을 나타냅니다.
>


## <a name="data-sources"></a>데이터 원본
소스 tooprovide 가시성 보안 상태에 따라 hello에서 데이터를 분석 하는 azure 보안 센터, 취약성을 식별 하 고 완화, 권장 있으며 활성 위협이 검색:

- Azure 서비스: 해당 서비스의 리소스 공급자와 통신 하 여 배포한 hello Azure 서비스 구성에 대 한 정보를 사용 합니다.
- 네트워크 트래픽: 원본/대상 IP/포트, 패킷 크기 및 네트워크 프로토콜과 같은 Microsoft의 인프라에서 샘플링된 네트워크 트래픽 메타데이터를 사용합니다.
- 파트너 솔루션: 방화벽 및 맬웨어 방지 솔루션과 같은 통합된 파트너 솔루션의 보안 경고를 사용합니다. 
- 가상 컴퓨터 및 서버: Windows 이벤트 및 감사 로그, IIS 로그, syslog 메시지 및 가상 컴퓨터의 크래시 덤프 파일과 같은 보안 이벤트에 대한 구성 정보 및 정보를 사용합니다. 또한 경고를 만들면 Azure 보안 센터 수 영향을 받는 hello VM 디스크의 스냅숏을 생성 되 고 컴퓨터 아티팩트 관련된 toohello 경고 범죄 분석을 위해 레지스트리 파일을 같이 hello VM 디스크 추출할 합니다.


## <a name="data-protection"></a>데이터 보호
**데이터 분리**: 데이터 hello 서비스 전체에서 각 구성 요소에 논리적으로 별도로 유지 됩니다. 모든 데이터에는 조직별로 태그가 지정됩니다. 이 태그 hello 데이터 수명 주기 동안 유지 되며 hello 서비스의 각 계층에서 적용 됩니다.

**데이터 액세스**:에서 주문 tooprovide 보안 권장 사항 및 보안 위협 조사, Microsoft 담당자에 수집 된 정보를 액세스 하거나 크래시 덤프 파일을 비롯 한 Azure 서비스를 사용 하 여 분석할 생성 이벤트를 처리 처리 VM 디스크 스냅샷 및 아티팩트 고객 데이터 또는 가상 컴퓨터의 개인 데이터가 의도 하지 않게 포함 될 수 있습니다. Toohello 준수 우리 [Microsoft 온라인 서비스 약관 및 개인정보취급방침](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), 상태 Microsoft가 고객 데이터를 사용 하 여 만들어지거나 광고 또는 유사한 상업적 목적에서 정보를 파생 되지 않습니다. 만 고객 데이터를 사용 하 여 필요한 tooprovide 목적으로 서비스를 제공 호환 비롯 하 여 서비스는 Azure로 합니다. 모든 권한 tooCustomer 데이터를 유지 합니다.

**데이터 사용**: 패턴을 사용 하 여 Microsoft 및 위협 인텔리전스 표시를 여러 테 넌 트에서 tooenhance 취급 예방 및 감지 기능;에 설명 된 hello 개인 정보 행에 따라 이렇게 우리의 [개인 정보 문](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx)합니다.

## <a name="data-location"></a>데이터 위치

**사용자 중**: hello Geos, 다음에 대 한 작업 영역 지정 되 고, 크래시 덤프 및 일부 유형의 경고 데이터를 포함 하 여 Azure 가상 컴퓨터에서 수집 된 데이터 작업 영역에 가장 가까운 hello에 저장 됩니다. 

| VM 지역                        | 작업 영역 지역 |
|-------------------------------|---------------|
| 미국, 브라질, 캐나다 | 미국 |
| 유럽, 영국        | 유럽        |
| 아시아 태평양, 일본, 인도    | 아시아 태평양  |
| 오스트레일리아                     | 오스트레일리아     |

 
VM 디스크 스냅샷 hello에 저장 된 hello VM 디스크와 동일한 저장소 계정입니다.
 
가상 컴퓨터와 다른 환경에서 실행 하는 서버에 대 한 예를 들어 온-프레미스에 hello 작업 영역 및 수집 된 데이터가 저장 되는 지역을 지정할 수 있습니다. 

**Azure 보안 센터 저장소**: 파트너 경고를 포함 한 경우 보안 경고에 대 한 정보는 지역별로 저장 된 반면 Azure 리소스와 관련 된 hello의 toohello 위치에 따라 보안 상태에 대 한 정보 및 권장 사항 hello United States 또는 toocustomer의 위치에 따라 유럽에 저장 됩니다.
Azure 보안 센터는 크래시 덤프 파일의 임시 복사본을 수집하고 이용 시도 및 손상 성공의 증거를 찾기 위해 분석합니다. Azure 보안 센터 내에서이 분석을 수행 합니다. 작업 영역에서 hello으로 같은 지역 hello 및 분석이 완료 되 면 삭제 hello 임시 복사본입니다.

컴퓨터 아티팩트 중앙에 저장 된 VM hello으로 같은 지역 hello 합니다. 


## <a name="managing-data-collection-from-virtual-machines"></a>가상 컴퓨터에서 데이터 컬렉션 관리

Azure에서 Security Center를 사용하는 경우 각 Azure 구독에 대해 데이터 수집이 활성화됩니다. 또한 hello Azure 보안 센터의 보안 정책 섹션에서에서 구독에 대 한 데이터 수집을 켤 수 있습니다. 데이터 수집 상태에서 Azure 가상 컴퓨터 및 만들어진 새로 프로 비전 hello Microsoft Monitoring Agent에 모든 기존 Azure 보안 센터 지원. 다양 한 보안을 검색 하는 hello Microsoft Monitoring agent 관련 구성 및 이벤트로 [Windows 용 이벤트 추적](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) 추적 (ETW). 또한 운영 체제 hello hello 과정 hello 컴퓨터를 실행 하는 동안 이벤트 로그 이벤트를 발생 합니다. 이러한 데이터의 예: 운영 체제 유형 및 버전, 운영 체제 로그(Windows 이벤트 로그), 프로세스 실행, 컴퓨터 이름, IP 주소, 로그인된 사용자 및 테넌트 ID입니다. Microsoft Monitoring Agent hello 이벤트 로그 항목을 읽고 ETW 추적 및 분석을 위해 tooyour 중에 복사 합니다. Microsoft Monitoring Agent hello 크래시 덤프 파일 tooyour 중에도 복사 합니다.

Azure 보안 센터 Free를 사용 하는 경우에 hello 보안 정책에서에서 가상 컴퓨터에서 데이터 수집을 해제할 수 있습니다. 데이터 수집 hello 표준 계층에 구독이 필요 합니다. VM 디스크 스냅숏 및 아티팩트 컬렉션은 데이터 수집이 사용하지 않도록 설정된 경우에도 여전히 사용하도록 설정됩니다.


## <a name="see-also"></a>참고 항목
이 문서에서는 Azure 보안 센터에서 데이터 관리하고 보호하는 방법을 알아봅니다. Azure 보안 센터에 대해 자세히 toolearn 참조:

* [Azure 보안 센터 계획 및 운영 가이드](security-center-planning-and-operations-guide.md) -학습 방법을 tooplan hello 디자인 고려 사항 tooadopt Azure 보안 센터를 이해 하 고 있습니다.
* [Azure 보안 센터에서 보안 상태 모니터링](security-center-monitoring.md) -toomonitor Azure 리소스의 상태를 hello 하는 방법에 대해 알아봅니다
* [Azure 보안 센터에서 경고를 관리 하 고 응답 toosecurity](security-center-managing-and-responding-alerts.md) -학습 방법을 toomanage 및 응답 toosecurity 경고
* [Azure 보안 센터를 사용 하 여 파트너 솔루션 모니터링](security-center-partner-solutions.md) -toomonitor 파트너 솔루션의 상태를 hello 하는 방법에 대해 알아봅니다.
* [Azure 보안 센터 FAQ](security-center-faq.md) -찾기 hello 서비스를 사용 하는 방법에 대 한 질문과 대답
* [Azure 보안 블로그](http://blogs.msdn.com/b/azuresecurity/) — Azure 보안 및 규정 준수에 관한 블로그 게시물을 찾습니다.
