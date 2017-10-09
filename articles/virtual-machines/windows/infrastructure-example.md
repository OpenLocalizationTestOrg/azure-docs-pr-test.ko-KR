---
title: "Azure 인프라 연습 aaaExample | Microsoft Docs"
description: "Hello 핵심 디자인 및 구현 지침 Azure에서 예제 인프라를 배포 하기 위한 방법을 알아봅니다."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a>Windows VM에 대한 Azure 인프라 연습 예제

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

이 문서에서는 예제 응용 프로그램 인프라를 구축하는 과정을 안내합니다. 모든 hello 지침과 명명 규칙, 가용성 집합, 가상 네트워크 및 부하 분산 장치에 의사 결정을 함께 제공 하는 간단한 온라인 상점에 대 한 인프라를 디자인 하 고 가상 컴퓨터 (Vm)를 배포 실제로 우리 자세히 설명 합니다.

## <a name="example-workload"></a>워크로드 예제
Adventure Works Cycles가 toobuild 구성 된 Azure에서 온라인 스토어 응용 프로그램:

* 웹 계층의 프런트 엔드 hello 클라이언트를 실행 하는 두 개의 IIS 서버
* 응용 프로그램 계층에 있으며 데이터 및 주문을 처리하는 두 IIS 서버
* 데이터베이스 계층에 제품 데이터 및 주문을 저장하기 위한 AlwaysOn 가용성 그룹(두 SQL Server 및 주 노드 감시) 이 있는 두 개의 Microsoft SQL Server 인스턴스
* 인증 계층에 있는 고객 계정 및 공급자에 대한 두 Active Directory 도메인 컨트롤러
* 서브넷인에 속하는 모든 hello 서버:
  * 웹 서버 hello에 대 한 프런트 엔드 서브넷 
  * hello 응용 프로그램 서버, SQL 클러스터 및 도메인 컨트롤러에 대 한 백 엔드 서브넷

![응용 프로그램 인프라의 여러 다른 계층 다이어그램](./media/infrastructure-example/example-tiers.png)

보안 들어오는 웹 트래픽의 같아야 hello 웹 서버 간에 부하 분산 된 고객 hello 온라인 스토어를 검색할 합니다. 서버 hello 응용 프로그램 서버 사이에서 균형을 맞춰야 hello 웹에서 주문 hello 형식의 HTTP 트래픽을 처리를 요청 합니다. 또한 고가용성을 위해 hello 인프라를 설계 해야 합니다.

hello 결과 디자인에 통합 되어 있어야 합니다.

* Azure 구독 및 계정
* 단일 리소스 그룹
* Azure Managed Disks
* 두 서브넷을 사용하는 가상 네트워크
* 비슷한 역할을 가진 Vm hello에 대 한 가용성 집합
* 가상 컴퓨터

위의 모든 hello 명명 규칙에 부합 합니다.

* Adventure Works Cycles는 **[IT 작업]-[위치]-[Azure 리소스]** 를 접두사로 사용합니다.
  * 예를 들어 "**azos**" (Azure 온라인 저장소)는 IT 워크 로드 이름을 hello 및 "**사용**"는 hello 위치 (미국 동부 2)
* 가상 네트워크는 AZOS-USE-VN**[숫자]**를 사용합니다.
* 가용성 집합은 azos-use-as-**[역할]**을 사용합니다.
* 가상 컴퓨터 이름은 azos-use-vm-**[VM 이름]**을 사용합니다.

## <a name="azure-subscriptions-and-accounts"></a>Azure 구독 및 계정
Adventure Works Cycles는 Adventure Works 엔터프라이즈 구독을이 IT 워크 로드에 대 한 청구 tooprovide 라는 자신의 엔터프라이즈 구독을 사용 합니다.

## <a name="storage"></a>저장소
Adventure Works Cycles에서는 Azure Managed Disks를 사용해야 한다고 결정했습니다. VM을 만들 때 사용 가능한 두 저장소 계층이 모두 사용됩니다.

* **표준 저장소** hello 웹 서버, 응용 프로그램 서버 및 도메인 컨트롤러 및 해당 데이터 디스크에 대 한 합니다.
* **프리미엄 저장소** hello SQL Server Vm 및 해당 데이터 디스크에 대 한 합니다.

## <a name="virtual-network-and-subnets"></a>가상 네트워크 및 서브넷
Hello 가상 네트워크는 진행 중인 연결 toohello Adventure 작업 Cycles 온-프레미스 네트워크를 필요 하지 않습니다, 클라우드 전용 가상 네트워크에서 결정 합니다.

자신이 만든 다음 hello Azure 포털을 사용 하 여 설정을 hello로 클라우드 전용 가상 네트워크:

* 이름: AZOS-USE-VN01
* 위치: East US 2
* 가상 네트워크 주소 공간: 10.0.0.0/8
* 첫 번째 서브넷:
  * 이름: FrontEnd
  * 주소 공간: 10.0.1.0/24
* 두 번째 서브넷:
  * 이름: BackEnd
  * 주소 공간: 10.0.2.0/24

## <a name="availability-sets"></a>가용성 집합
온라인 상점별 4 개 가용성 집합을 결정된 Adventure Works Cycles의 모든 4 개 계층의 고가용성을 toomaintain:

* **웹으로 azos 사용** hello 웹 서버에 대 한
* **앱으로 azos 사용** hello 응용 프로그램 서버에 대 한
* **sql로 azos 사용** SQL 서버 hello에 대 한
* **dc로 azos 사용** hello 도메인 컨트롤러에 대 한

## <a name="virtual-machines"></a>가상 컴퓨터
Adventure Works Cycles의 Azure Vm에 대 한 이름 다음 hello 결정:

* **사용 하 여 vm web01 azos** hello 첫 번째 웹 서버에 대 한
* **사용 하 여 vm web02 azos** hello 두 번째 웹 서버에 대 한
* **사용 하 여 vm app01 azos** hello 첫 번째 응용 프로그램 서버에 대 한
* **사용 하 여 vm app02 azos** hello 두 번째 응용 프로그램 서버에 대 한
* **사용 하 여 vm sql01 azos** hello 클러스터의 첫 번째 SQL Server 서버 hello에 대 한
* **사용 하 여 vm sql02 azos** hello 클러스터의 두 번째 SQL Server 서버 hello에 대 한
* **사용 하 여 vm dc01 azos** hello 첫 번째 도메인 컨트롤러에 대 한
* **azos 02로 사용 하 여-vm-복제** hello 두 번째 도메인 컨트롤러에 대 한

다음은 hello 결과 구성입니다.

![Azure에 배포되는 최종 응용 프로그램 인프라](./media/infrastructure-example/example-config.png)

이 구성은 다음을 통합합니다.

* 두 서브넷을 사용하는 클라우드 전용 가상 네트워크(프런트 엔드 및 백 엔드)
* Standard 디스크와 Premium 디스크가 둘 다 있는 Azure Managed Disks
* Hello 온라인 상점의 각 계층에 대해 하나씩 네 개의 가용성 집합
* hello 4 계층에 대 한 hello 가상 컴퓨터
* Hello 인터넷 toohello 웹 서버에서 웹 HTTPS 기반 트래픽에 대 한 외부 부하 분산 된 집합
* 내부 부하 분산 집합 hello 웹 서버 toohello 응용 프로그램 서버에서 암호화 되지 않은 웹 트래픽에 대 한
* 단일 리소스 그룹