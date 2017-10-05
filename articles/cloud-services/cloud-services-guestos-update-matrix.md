---
title: "최신 Azure 게스트 OS 릴리스에 대해 알아보기 | Microsoft Docs"
description: "Azure  Cloud Services 게스트 OS에 대한 최신 릴리스 뉴스 및 SDK 호환성."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 6306cafe-1153-44c7-8554-623b03d59a34
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 8/24/2017
ms.author: raiye
ms.openlocfilehash: a4439346817df9223c032abc1405a7cf9cbe780b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스
Cloud Services용 최신 Azure 게스트 OS릴리스에 대한 최신 정보를 제공합니다. 이 정보는 게스트 OS를 사용하지 않도록 설정하기 전에 업그레이드 경로를 계획하는 데 도움이 됩니다. [Azure 게스트 OS 업데이트 설정][Azure Guest OS Update Settings]의 설명에 따라 *자동* 게스트 OS 업데이트를 사용하도록 역할을 구성하는 경우, 이 페이지를 읽지 않아도 됩니다.

> [!IMPORTANT]
> 이 페이지는 게스트 OS를 기반으로 실행하는 Cloud Services 웹 및 작업자 역할에 적용됩니다. IaaS Virtual Machines에 **적용되지 않습니다** .
>
>


> [!NOTE]
> RSS 피드는 최근에 사용되지 않습니다. 곧 제공될 새 피드에 대한 업데이트에 대해 알아봅니다.
>
>

게스트 OS가 무엇인지 또는 게스트 OS 릴리스가 어떻게 작동하는지 잘 모르시나요? [이](#how-it-works) 섹션을 읽어보세요.

## <a name="news-updates"></a>새 업데이트

###### <a name="august-24-2017"></a>**2017년 8월 24일**
8월 게스트 OS가 릴리스되었습니다.

###### <a name="august-3-2017"></a>**2017년 8월 3일**
7월 게스트 OS가 릴리스되었습니다.

###### <a name="july-19-2017"></a>**2017년 7월 19일**
게스트 OS 7월 롤아웃은 7월 19일에 시작되며 8월 8일에 출시될 예정입니다.

###### <a name="july-7-2017"></a>**2017년 7월 7일**
6월 게스트 OS가 릴리스되었습니다.

###### <a name="june-16-2017"></a>**2017년 6월 16일**
게스트 OS 6월 롤아웃은 6월 16일에 시작되며 7월 11일에 출시될 예정입니다.

###### <a name="june-5-2017"></a>**2017년 6월 5일**
게스트 OS 5월이 릴리스되었습니다.

###### <a name="may-17-2017"></a>**2017년 5월 17일**
보안 버그로 인해 포털에서 [수정 사항]이 없는 2016년 12월 및 2017년 1월 OS 릴리스를 사용하지 않습니다. WA-GUEST-OS-5.4_201612-01, WA-GUEST-OS-4.39_201612-01, WA-GUEST-OS-3.46_201612-01, WA-GUEST-OS-2.59_201701-01

###### <a name="may-12-2017"></a>**2017년 5월 12일**
게스트 OS 5월 롤아웃은 5월 12일에 시작되며 6월 13일에 출시될 예정입니다.

###### <a name="april-18-2017"></a>**2017년 4월 18일**
게스트 OS 4월 롤아웃은 4월 18일에 시작되며 5월 9일에 출시될 예정입니다.

###### <a name="april-10-2017"></a>**2017년 4월 10일**
게스트 OS 3월 롤아웃은 2017년 3월 14일에 시작되었으며 2017년 4월 10일에 출시되었습니다.

###### <a name="january-10-2017"></a>**2017년 1월 10일**
1월 게스트 OS에는 OS 제품군 2(Windows 2008 Server R2)에만 영향을 미치는 패치가 포함되어 있습니다. 따라서 이번 달에는 OS 제품군 2 이미지(WA-GUEST-OS-2.59_201701-01)만 릴리스했습니다. 모든 다른 OS 제품군의 경우 12월 OS(201612-01)는 최신 상태를 유지합니다.


## <a name="releases"></a>릴리스
## <a name="family-5-releases"></a>제품군 5 릴리스
**Windows Server, 2016**

설치된 .NET Framework: 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2

> [!NOTE]
> 별표(*)가 표시된 날짜는 변경될 수 있음
>
> OS 제품군 5의 RDP 암호는 10자 이상이어야 합니다.
>

| 구성 문자열 | 릴리스 날짜 | 비활성화 날짜 | 만료 날짜 |
| --- | --- | --- | --- |
| WA-GUEST-OS-5.10_201708-01 |2017년 8월 24일 |5.12 후 |TBD |
| WA-GUEST-OS-5.9_201707-01 |2017년 8월 3일 |Post 5.11 |TBD |
| WA-GUEST-OS-5.8_201706-01 |2017년 7월 7일 |Post 5.10 |TBD |
|~~WA-GUEST-OS-5.7_201705-01~~ |2017년 6월 5일 |2017년 8월 24일 |TBD |
|~~WA-GUEST-OS-5.6_201704-01~~ |2017년 5월 9일 |2017년 8월 3일 |TBD |
|~~WA-GUEST-OS-5.5_201703-01~~ |2017년 4월 10일 |2017년 7월 7일 |TBD |
|~~WA-GUEST-OS-5.4_201612-01~~ |2017년 1월 10일 |2017년 6월 5일|TBD |
|~~WA-GUEST-OS-5.3_201611-01~~ |2016년 12월 14일 |2017년 5월 9일 |TBD |
|~~WA-GUEST-OS-5.2_201610-02~~ |2016년 11월 1일 |2017년 4월 10일 |TBD |

## <a name="family-4-releases"></a>제품군 4 릴리스
**Windows Server 2012 R2**

.NET 4.0, 4.5, 4.5.1, 4.5.2 지원

> [!NOTE]
> *가 표시된 날짜는 변경될 수 있음
>
>

| 구성 문자열 | 릴리스 날짜 | 비활성화 날짜 | 만료 날짜 |
| --- | --- | --- | --- |
| WA-GUEST-OS-4.45_201708-01 |2017년 8월 24일 |4.47 후 |TBD |
| WA-GUEST-OS-4.44_201707-01 |2017년 8월 3일 |Post 4.46 |TBD |
| WA-GUEST-OS-4.43_201706-01 |2017년 7월 7일 |Post 4.45 |TBD |
|~~WA-GUEST-OS-4.42_201705-01~~ |2017년 6월 5일 |2017년 8월 24일 |TBD |
|~~WA-GUEST-OS-4.41_201704-01~~ |2017년 5월 9일 |2017년 8월 3일 |TBD |
|~~WA-GUEST-OS-4.40_201703-01~~ |2017년 4월 10일 |2017년 7월 7일 |TBD |
|~~WA-GUEST-OS-4.39_201612-01~~ |2017년 1월 10일 |2017년 6월 5일 |TBD |
|~~WA-GUEST-OS-4.38_201611-01~~ |2016년 12월 14일 |2017년 5월 9일 |TBD |
|~~WA-GUEST-OS-4.37_201610-02~~ |2016년 11월 16일 |2017년 4월 10일 |TBD |
|~~WA-GUEST-OS-4.36_201609-01~~ |2016년 10월 13일 |2017년 1월 14일 |TBD |
|~~WA-GUEST-OS-4.35_201608-01~~ |2016년 9월 13일 |2016년 12월 16일 |TBD |
|~~WA-GUEST-OS-4.34_201607-01~~ |2016년 8월 8일 |2016년 11월 13일 |TBD |


## <a name="family-3-releases"></a>제품군 3 릴리스
**Windows Server 2012**

.NET 4.0, 4.5, 4.5.1, 4.5.2 지원

> [!NOTE]
> *가 표시된 날짜는 변경될 수 있음
>
>

| 구성 문자열 | 릴리스 날짜 | 비활성화 날짜 | 만료 날짜 |
| --- | --- | --- | --- |
| WA-GUEST-OS-3.52_201708-01 |2017년 8월 24일 |3.54 후 |TBD |
| WA-GUEST-OS-3.51_201707-01 |2017년 8월 3일 |Post 3.53 |TBD |
| WA-GUEST-OS-3.50_201706-01 |2017년 7월 7일 |Post 3.52 |TBD |
|~~WA-GUEST-OS-3.49_201705-01~~ |2017년 6월 5일 |2017년 8월 24일 |TBD |
|~~WA-GUEST-OS-3.48_201704-01~~ |2017년 5월 9일 |2017년 8월 3일 |TBD |
|~~WA-GUEST-OS-3.47_201703-01~~ |2017년 4월 10일 |2017년 7월 7일 |TBD |
|~~WA-GUEST-OS-3.46_201612-01~~ |2017년 1월 10일 |2017년 6월 5일 |TBD |
|~~WA-GUEST-OS-3.45_201611-01~~ |2016년 12월 14일 |2017년 5월 9일 |TBD |
|~~WA-GUEST-OS-3.44_201610-02~~ |2016년 11월 16일 |2017년 5월 1일 |TBD |
|~~WA-GUEST-OS-3.43_201609-01~~ |2016년 10월 13일 |2017년 1월 14일 |TBD |
|~~WA-GUEST-OS-3.42_201608-01~~ |2016년 9월 13일 |2016년 12월 16일 |TBD |
|~~WA-GUEST-OS-3.41_201607-01~~ |2016년 8월 8일 |2016년 11월 13일 |TBD |


## <a name="family-2-releases"></a>제품군 2 릴리스
**Windows Server 2008 R2 SP1**

.NET 3.5, 4.0, 4.5, 4.5.1, 4.5.2 지원

> [!NOTE]
> *가 표시된 날짜는 변경될 수 있음
>
>

| 구성 문자열 | 릴리스 날짜 | 비활성화 날짜 | 만료 날짜 |
| --- | --- | --- | --- |
| WA-GUEST-OS-2.65_201708-01 |2017년 8월 24일 |2.67 후 |TBD |
| WA-GUEST-OS-2.64_201707-01 |2017년 8월 3일 |Post 2.66 |TBD |
| WA-GUEST-OS-2.63_201706-01 |2017년 7월 7일 |Post 2.65 |TBD |
|~~WA-GUEST-OS-2.62_201705-01~~ |2017년 6월 5일 |2017년 8월 24일 |TBD |
|~~WA-GUEST-OS-2.61_201704-01~~ |2017년 5월 9일 |2017년 8월 3일 |TBD |
|~~WA-GUEST-OS-2.60_201703-01~~ |2017년 4월 10일 |2017년 7월 7일 |TBD |
|~~WA-GUEST-OS-2.59_201701-01~~ |2017년 1월 10일 |2017년 6월 5일 |TBD |
|~~WA-GUEST-OS-2.58_201612-01~~ |2017년 1월 10일 |2017년 5월 9일|TBD |
|~~WA-GUEST-OS-2.57_201611-01~~ |2016년 12월 14일 |2017년 4월 10일 |TBD |
|~~WA-GUEST-OS-2.56_201610-02~~ |2016년 11월 16일 |2017년 2월 10일 |TBD |
|~~WA-GUEST-OS-2.55_201609-01~~ |2016년 10월 13일 |2017년 1월 14일 |TBD |
|~~WA-GUEST-OS-2.54_201608-01~~ |2016년 9월 13일 |2016년 12월 16일 |TBD |
|~~WA-GUEST-OS-2.53_201607-01~~ |2016년 8월 8일 |2016년 11월 13일 |TBD |



## <a name="msrc-patch-updates"></a>MSRC 패치 업데이트
매달 각 게스트 OS 릴리스에 포함된 패치 목록은 [여기][patches]에서 사용 가능합니다.

## <a name="sdk-support"></a>SDK 지원
[Azure SDK에 대한 사용 중지 정책][retire policy sdk]에 2.2 이후 버전만 지원된다고 나와 있더라도 특정 게스트 OS 제품군을 통해 이전 버전을 사용할 수 있습니다. 항상 지원되는 최신 SDK를 사용해야 합니다.

| 게스트 OS 제품군 | 호환되는 SDK 버전 |
| --- | --- |
| 5 |버전 2.9.5.1+ |
| 4 |버전 2.1 이상 |
| 3 |버전 1.8 이상 |
| 2 |버전 1.3 이상 |
| 1 |버전 1.0 이상 |

## <a name="guest-os-release-information"></a>게스트 OS 릴리스 정보
게스트 OS 릴리스에 있어서 중요한 날짜 세 개는 **릴리스** 날짜, **비활성화** 날짜 및 **만료** 날짜입니다. 포털에 있고 대상 게스트 OS로 선택할 수 있는 게스트 OS는 사용 가능한 것으로 간주됩니다. 게스트 OS가 **비활성화** 날짜에 도달하면 Azure에서 제거됩니다. 그러나 해당 게스트 OS를 대상으로 하는 모든 클라우드 서비스는 계속 정상적으로 작동합니다.

**비활성화** 날짜와 **만료** 날짜 사이의 기간 동안 한 게스트 OS에서 다른 게스트 OS로 간편하게 전환할 수 있습니다. 게스트 OS로 *자동* 을 사용하는 경우 항상 최신 버전이 유지되므로 만료에 대해 걱정할 필요가 없습니다.

**만료** 날짜가 지났는데 여전히 해당 게스트 OS를 사용 중인 Cloud Service는 중지, 삭제 또는 강제 업그레이드됩니다. 사용 중지 정책에 대한 자세한 내용은 [여기][retirepolicy]서 확인할 수 있습니다.

## <a name="guest-os-family-version-explanation"></a>게스트 OS 제품군 버전 설명
게스트 OS 제품군은 출시된 Microsoft Windows Server 버전을 기반으로 합니다. 게스트 OS는 Azure Cloud Services가 실행되는 기본 운영 체제입니다. 각 게스트 OS에는 제품군, 버전 및 릴리스 번호가 있습니다.

* **Guest OS family**  
  은 게스트 OS가 기반으로 하는 Windows Server 운영 체제 릴리스입니다. 예를 들어 *제품군 3* 은 Windows Server 2012를 기반으로 합니다.
* **게스트 OS 버전**  
  새 게스트 OS 버전이 생성되는 날짜에 사용 가능한 게스트 OS 제품군 이미지 및 관련 MSRC([Microsoft 보안 대응 센터)][msrc] 패치로 한정됩니다. 일부 패치는 포함될 수 있습니다.

    0에서 시작하고 새 업데이트 집합이 추가 될 때마다 1씩 증가하는 숫자입니다. 중요한 경우.후행 0만 표시됩니다. 즉, 버전 2.10은 다르며, 버전 2.1 버전보다 더 한참 후의 버전입니다.
* **게스트 OS 릴리스**  
  게스트 OS 버전의 릴리스입니다. 필요한 변경 내용을 테스트하는 동안 Microsoft가 문제를 발견하는 경우에 릴리스가 발생합니다. 최신 릴리스는 항상 이전의 모든 릴리스를 공개이든 또는 비공개이든 대체합니다. Azure Portal에서 사용자는 지정된 버전에 대한 최신 릴리스를 선택할 수만 있습니다. 이전 릴리스에서 실행 중인 배포는 일반적으로 버그의 심각도 따라 강제 업그레이드되지 않습니다.

아래 예제에서 2는 제품군이며, 12는 버전이고 "rel2"는 릴리스입니다.

**게스트 OS 릴리스** -2.12 rel2

**이 릴리스에 대한 구성 문자열** -WA-GUEST-OS-2.12_201208-02

게스트 OS에 대한 구성에는 문자열에서 보여주는 MSRC 패치가 해당 릴리스에 대한 것으로 간주된 날짜와 함께 여기에 포함된 동일한 정보가 있습니다. 이 예에서는 Windows Server 2008 R2에 대한 MSRC 패치가 생성되며 2012년 8월포함이 고려되었습니다. 특히 해당 버전의 Windows Server에 적용되는 패치만 포함됩니다. 예를 들어 MSRC 패치가 Microsoft office에 적용되는 경우, 해당 제품이 Windows Server 기본 이미지의 일부가 아니므로 포함되지 않습니다.

## <a name="guest-os-system-update-process"></a>게스트 OS 시스템 업데이트 프로세스
이 페이지에 예정된 게스트 OS 릴리스에 대한 정보가 포함됩니다. "자동" 업데이트로 설정된 경우 해당 클라우드 서비스 역할이 다시 부팅되기때문에 릴리스가 발생하는 시기를 알고 싶어하는지 표시합니다. 게스트 OS 릴리스는 매달 두째 주 화요일에 발생하는 MSRC 업데이트 릴리스 5일 후에 발생합니다. 새 릴리스는 각 게스트 OS 제품군에 대한 모든 관련 MSRC 패치를 포함합니다.

Microsoft Azure는 지속적으로 업데이트를 릴리스하고 있습니다. 이러한 업데이트로 게스트 OS가 파이프라인에서 유일합니다. 릴리스는 다양한 요인에 의해 영향을 받을 수 있어 나열할 수 없습니다. 또한 Azure는 수백 대의 컴퓨터에서 실행 됩니다. 역할이 다시 부팅 되는 정확한 날짜와 시간을 제공할 수 있다는 것을 의미합니다. 제한 또는 시간 재부팅에 대한 계획을 설정하고 있습니다.

게스트 OS의 새 릴리스를 게시하는 경우 Azure에 완전히 전파하는데 시간이 걸릴 수 있습니다. 서비스가 새 게스트 OS에 대해 업데이트되므로 업데이트 도메인을 구분하지 않고 다시 부팅됩니다. "자동" 업데이트를 사용하도록 설정된 서비스가 처음 릴리스됩니다. 업데이트 후 Azure Portal에서 서비스에 대해 나열된 새 게스트 OS 버전을 볼 수 있습니다. 이 기간 동안 다시 릴리스할 수 있습니다. 일부 버전은 오랜 시간을 통해 배포할 수 있으며 공식 릴리스 날짜 이후 수 주 동안 자동 업그레이드 재부팅이 발생하지 않을 수 있습니다. 게스트 OS를 사용할 수 있으면, 구성 파일이나 포털에서 해당 버전을 명시적으로 찾을 수 있습니다.

게스트 및 호스트 OS 업데이트의 기술 세부 정보에 대한 포인터 및 시작에 관한 중요 정보 처리는 [OS 업그레이드로 인한 역할 인스턴스 다시 시작][restarts]이라는 MSDN 블로그 게시물을 참조하세요.

게스트 OS를 수동으로 업데이트하는 경우 추가 정보는 [게스트 OS 사용 중지 정책][retirepolicy]을 참조하세요.

## <a name="guest-os-supportability-and-retirement-policy"></a>게스트 OS 지원 가능성 및 사용 중지 정책
게스트 OS 지원 가능성 및 사용 중지 정책은 [여기][retirepolicy]에 설명됩니다.

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure.md
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
[수정 사항]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
