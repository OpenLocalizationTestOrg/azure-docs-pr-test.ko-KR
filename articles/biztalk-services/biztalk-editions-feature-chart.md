---
title: "BizTalk 서비스 버전의 기능에 대해 aaaLearn | Microsoft Docs"
description: "Hello BizTalk 서비스 버전의 hello 기능을 비교한: 무료, Developer, Basic, Standard 및 Premium입니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>BizTalk 서비스: 버전 차트

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk 서비스는 여러 버전을 제공합니다. 이 문서 toodetermine은 시나리오 및 비즈니스 요구에 따라 사용 합니다.

## <a name="compare-hello-editions"></a>Hello 버전 비교
**Free(Preview)**

하이브리드 연결을 만들고 관리하는 기능이 포함되어 있습니다. 하이브리드 연결을 쉽게 tooconnect Azure 웹 사이트 tooan 온-프레미스 SQL Server와 같은 시스템입니다.

**Developer**

하이브리드 연결, 사용하기 쉬운 거래 업체 관리 포털을 통한 EAI 및 EDI 메시지 처리, X12와 AS2를 통한 다양한 EDI 처리 및 공통 EDI 스키마 지원 등의 기능이 포함되어 있습니다. 모든 HTTP/S, REST, FTP, WCF 및 SFTP 프로토콜 tooread로 hello 클라우드의 서비스를에서 연결 하는 일반적인 EAI 시나리오를 만들고 메시지를 쓸 수 있습니다.  즉시 사용 SAP, Oracle eBusiness, Oracle DB, Siebel 및 SQL Server 어댑터로 tooon 온-프레미스 LOB 시스템에 연결을 사용 합니다. Visual Studio 도구가 포함된 개발자 중심 환경을 사용하여 손쉽게 개발하고 배포할 수 있습니다. 제한 된 toodevelopment 및 테스트 용도로와 없습니다 서비스 수준 계약 (SLA).

**Basic**

하이브리드 연결, EAI 브리지, EDI 규약 및 BizTalk Adapter Pack 연결에서는 대부분의 증가 사용 하는 hello 개발자 기능을 포함합니다. 또한 고가용성 및 hello 옵션 tooscale는 서비스 수준 계약 (SLA)을 제공합니다.

**Standard**

하이브리드 연결, EAI 브리지, EDI 규약 및 BizTalk Adapter Pack 연결에 증가 모든 hello 기본 기능을 포함합니다. 또한 고가용성 및 hello 옵션 tooscale는 서비스 수준 계약 (SLA)을 제공합니다.

**Premium**

하이브리드 연결, EAI 브리지, EDI 규약 및 BizTalk Adapter Pack 연결 증가 hello 표준 기능을 모두 포함합니다. 보관, 높은 가용성 및 hello 옵션 tooscale는 서비스 수준 계약 (SLA)도 포함 됩니다.

## <a name="editions-chart"></a>버전 차트
hello 다음 표에서 hello 이러한 차이점을 나열 합니다.

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Free(Preview)</th>
        <th>Developer</th>
        <th>Basic</th>
        <th>Standard</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>시작 가격</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011"> Azure BizTalk Services 가격 책정</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full">Azure 요금 계산기</a></td>
</tr>
<tr>
<td><strong>기본 최소 구성</strong></td>
<td>Free 장치 1개</td>
<td>Developer 장치 1개</td>
<td>Basic 장치 1개</td>
<td>Standard 장치 1개</td>
<td>Premium 장치 1개</td>
</tr>
<tr>
<td><strong>규모</strong></td>
<td>확장 안 함</td>
<td>확장 안 함</td>
<td>1 Basic 장치씩 확장함</td>
<td>1 표준 장치씩 확장함</td>
<td>1 프리미엄 장치씩 확장함</td>
</tr>
<tr>
<td><strong>최대 허용 규모 확장</strong></td>
<td>확장 안 함</td>
<td>확장 안 함</td>
<td>Too8 단위를</td>
<td>Too8 단위를</td>
<td>Too8 단위를</td>
</tr>
<tr>
<td><strong>장치당 EAI 브리지</strong></td>
<td>포함되지 않음</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
TPM 계약 포함</td>
<td>포함되지 않음</td>
<td>포함됨. 장치당 계약 10개</td>
<td>포함됨. 장치당 계약 50개</td>
<td>포함됨. 장치당 계약 250개</td>
<td>포함됨. 장치당 계약 1000개</td>
</tr>
<tr>
<td><strong>장치당 하이브리드 연결 수</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>장치당 하이브리드 연결 데이터 전송(GB)</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>BizTalk 어댑터 서비스 연결 tooon 온-프레미스 LOB 시스템</strong></td>
<td>포함되지 않음</td>
<td>1개 연결</td>
<td>2개 연결</td>
<td>5개 연결</td>
<td>25개 연결</td>
</tr>
<tr>
<td align="left"><strong>지원되는 프로토콜/시스템:</strong>
<ul>
<li>http</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>SB(서비스 버스)</li>
<li>Azure Blob</li>
<li>REST API</li>
</ul>
</td>
<td>포함되지 않음</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
</tr>
<tr>
<td><strong>고가용성</strong>
<br/><br/>
Service Level Agreement(서비스 수준 약정)는 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Azure BizTalk Services 가격 책정</a>을 참조하세요.
</td>
<td>포함되지 않음</td>
<td>포함되지 않음</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
</tr>
<tr>
<td><strong>백업 및 복원</strong></td>
<td>포함되지 않음</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
</tr>
<tr>
<td><strong>추적</strong></td>
<td>포함되지 않음</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
</tr>
<tr>
<td><strong>보관</strong><br/><br/>
추적 메시지 다운로드 및 NRR(수신 부인 방지) 포함</td>
<td>포함되지 않음</td>
<td>포함됨</td>
<td>포함되지 않음</td>
<td>포함되지 않음</td>
<td>포함됨</td>
</tr>
<tr>
<td><strong>사용자 지정 코드 사용</strong></td>
<td>포함되지 않음</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
</tr>
<tr>
<td><strong>변환 사용(사용자 지정 XSLT 포함)</strong></td>
<td>포함되지 않음</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
<td>포함됨</td>
</tr>
</table>

> [!NOTE]
> 하드웨어 오류에 대한 복원력을 위해 고가용성은 단일 BizTalk 장치 내에 반드시 VM을 여러 개 가집니다.
> 
> 

## <a name="faqs"></a>FAQ
#### <a name="what-is-a-biztalk-unit"></a>BizTalk 장치란 무엇인가요?
"장치"는 Azure BizTalk 서비스 배포의 hello 원자성 수준입니다. 각 버전에는 계산 용량 및 메모리가 다른 장치가 제공됩니다. 예를 들어 Basic 장치는 Developer 장치보다 계산 용량이 더 크고, Standard 장치는 Basic 장치보다 계산 용량이 더 크며 등등합니다. BizTalk 서비스를 확장할 때 장치로 확장합니다.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>BizTalk 서비스와 Azure BizTalk VM 간의 hello 차이점은 무엇입니까?
BizTalk 서비스는 hello 클라우드에서 통합 솔루션을 구축 하기 위한 진정한 플랫폼으로-서비스 (PaaS) 아키텍처를 제공 합니다. Hello PaaS 모델을 완전히 hello 응용 프로그램 논리에 집중 하 고이 hello 인프라 관리 tooMicrosoft 모두 포함 하 여:

* 필요 toomanage 또는 패치 가상 컴퓨터가 없습니다.
* Microsoft에서 가용성을 보증합니다.
* 눈금 단순히 더 요청 하 여 요청 시 또는 hello Azure 포털을 통해 작은 용량을 제어 합니다.

Azure 가상 컴퓨터의 BizTalk Server는 IaaS(Infrastructure-as-a-Service) 아키텍처를 제공합니다. 가상 컴퓨터를 만들고 온-프레미스 환경의와 동일 하 게 구성 코드 변경 없이 hello 클라우드에서 쉽게 toorun 기존 응용 프로그램을 만드는 합니다. IaaS를 여전히 hello 가상 컴퓨터를 구성 하 고, (예를 들어 소프트웨어를 설치 및 OS 패치) hello 가상 컴퓨터를 관리, 가용성을 높이기 위한 hello 응용 프로그램을 설계 해야 됩니다.

인프라 관리 노력을 최소화하는 새로운 통합 솔루션을 구축하려면 BizTalk 서비스를 사용하세요. Tooquickly를 조회 하는 경우 기존 BizTalk 솔루션을 마이그레이션하거나 주문형 환경 toodevelop 및 BizTalk Server 테스트 응용 프로그램을 사용 하 여 BizTalk Server는 Azure 가상 컴퓨터에서.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>BizTalk 어댑터 서비스 및 하이브리드 연결의 hello 차이점은 무엇입니까?
hello BizTalk 어댑터 서비스는 Azure BizTalk 서비스에서 사용 됩니다. hello BizTalk 어댑터 서비스는 hello BizTalk Adapter Pack tooconnect tooan 온-프레미스 업무 (LOB) 시스템을 사용합니다. 하이브리드 연결을 간편 하 고 편리한 tooconnect Azure 앱 서비스의 hello 웹 응용 프로그램 기능과 마찬가지로 Azure 응용 프로그램을 제공 및 Azure 모바일 서비스, tooan 온-프레미스 리소스입니다.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>"장치당 하이브리드 연결 데이터 전송(GB)"은 무엇을 의미하나요? 분/시간/일/주/월 단위입니까? Hello 제한에 도달 하면 어떻게 되나요?
하이브리드 연결 단가 hello hello BizTalk 서비스 버전에 따라 달라 집니다. 즉, 전송하는 데이터 양에 따라 비용이 달라집니다. 예를 들어 매일 10GB 데이터를 전송하는 것이 매일 100GB를 전송하는 것보다 비용이 적게 듭니다. 사용 하 여 hello [가격 계산기](https://azure.microsoft.com/pricing/calculator/?scenario=full) toodetermine 특정 비용을 BizTalk 서비스에 대 한 합니다. 일반적으로 매일 hello 한도가 적용 됩니다. Hello도 초과 하면 초과분 hello 속도로 $1 GB 당 대금이 청구 됩니다.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>BizTalk 서비스의 규약을 만들 때 이유는 브리지의 hello 수 위로 이동 하나가 아닌 두?
각 계약은 두 개의 다른 브리지(송신 측 통신 브리지와 수신 측 통신 브리지)로 구성되어 있습니다.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>브리지 또는 계약의 hello 수에 hello 할당량 한도 도달 하려면 어떻게 됩니까?
Toodeploy 수 없습니다. 모든 새 브리지 하거나 하는 어떤 새 계약을 만듭니다. 더 많은 toodeploy, tooscale hello BizTalk 서비스 또는 업그레이드 tooa 더 높은 버전의 toomore 단위를 해야합니다.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>BizTalk 서비스 tooanother의 한 계층에서 마이그레이션하려면 어떻게 해야 합니까?
hello 무료 버전을 백업할 수 없습니다 및 tooanother 계층 복원 마이그레이션된 또는 '수직' tooanother 계층 수 없습니다. 다른 계층 해야 할 경우 hello 새 계층을 사용 하 여 새 BizTalk 서비스를 만듭니다. 하이브리드 연결의 경우에 다시 작성 하는 필요성 toobe를 포함 하 여 hello 무료 버전을 사용 하 여 만든 모든 아티팩트가 새 BizTalk 서비스 hello 합니다. 

Hello 나머지 버전에 대 한 hello 백업을 사용 하 고 하나의 계층 tooanother에서 아티팩트 마이그레이션에 대 한 복원 합니다. 예를 들어 hello 표준 계층에 있는 아티팩트를 백업 하 고 복원할 toohello Premium 계층. [BizTalk 서비스: 백업 및 복원](biztalk-backup-restore.md) hello 지원 되는 마이그레이션 경로 설명 하 고 어떤 아티팩트 백업 나열 합니다. 하이브리드 연결이 백업되지 않는다는 점에 유의합니다. 백업 및 복원 tooa 새 계층을 한 후 다음을 다시 만들어야 hello 하이브리드 연결 합니다.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>Hello 서비스에 포함 된 BizTalk 어댑터 서비스 hello? Hello 소프트웨어를 받는 방법
BizTalk 어댑터 서비스 BizTalk 어댑터 팩 hello로 hello hello Azure BizTalk Services SDK에 포함 된 예, [다운로드](http://www.microsoft.com/download/details.aspx?id=39087)합니다.

## <a name="next-steps"></a>다음 단계
toocreate Azure BizTalk 서비스에서 Azure 포털, go를 너무 hello[BizTalk 서비스: Azure 포털 hello를 사용 하 여 프로 비전](biztalk-provision-services.md)합니다. 응용 프로그램을 이동 너무 만들 toostart[Azure BizTalk 서비스](http://go.microsoft.com/fwlink/p/?LinkID=235197)합니다.

## <a name="additional-resources"></a>추가 리소스
* [BizTalk 서비스: hello Azure 포털을 사용 하 여 프로 비전](biztalk-provision-services.md)<br/>
* [BizTalk 서비스: 프로비저닝 상태 차트](biztalk-service-state-chart.md)<br/>
* [BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Backup and restore](biztalk-backup-restore.md)<br/>
* [BizTalk 서비스: 제한](biztalk-throttling-thresholds.md)<br/>
* [BizTalk 서비스: 발급자 이름 및 발급자 키](biztalk-issuer-name-issuer-key.md)<br/>
* [Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

