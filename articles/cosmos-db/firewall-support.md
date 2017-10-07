---
title: "액세스 제어 aaaAzure Cosmos DB 방화벽 지원 및 IP | Microsoft Docs"
description: "방화벽에 대 한 toouse IP 액세스 제어 정책을 Azure Cosmos DB 데이터베이스 계정에 지 원하는 방법에 대해 알아봅니다."
keywords: "IP 액세스 제어, 방화벽 지원"
services: cosmos-db
author: shahankur11
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: c1b9ede0-ed93-411a-ac9a-62c113a8e887
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ankshah
ms.openlocfilehash: b5cdbdb28e9d7ee0fd0ea54aad277167b699929f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-firewall-support"></a>Azure Cosmos DB 방화벽 지원
Azure Cosmos DB 데이터베이스 계정에 저장 된 toosecure 데이터, Azure Cosmos DB 제공한 지원을 기반으로 하는 암호에 대 한 [권한 부여 모델](https://msdn.microsoft.com/library/azure/dn783368.aspx) HMAC ()는 강력한 해시 기반 메시지 인증 코드를 활용 하 합니다. 이제 또한 toohello 암호 기반 인증 모델, Azure Cosmos DB 정책 기반 인바운드 방화벽 지원에 대 한 IP 기반 액세스 제어를 지원 합니다. 이 모델 기존의 데이터베이스 시스템의 toohello 방화벽 규칙을 매우 유사 하며 추가 수준의 보안 toohello Azure Cosmos DB 데이터베이스 계정을 제공 합니다. 이 모델에는 Azure Cosmos DB 데이터베이스 계정 toobe는 승인 된 컴퓨터 집합에만 액세스할 수 있는 구성 하거나 클라우드 서비스 이제 있습니다. 이러한 승인 된 컴퓨터 및 서비스 집합에서 tooAzure Cosmos DB 리소스에 액세스는 여전히 hello 호출자 toopresent 유효한 권한 부여 토큰이 필요합니다.

## <a name="ip-access-control-overview"></a>IP 액세스 제어 개요
기본적으로 Azure Cosmos DB 데이터베이스 계정은 hello 요청은과 함께 유효한 권한 부여 토큰으로 공용 인터넷에서 액세스할 수입니다. tooconfigure IP 정책 기반 액세스 제어 hello 사용자 IP 주소 또는 IP 주소 범위에 hello 허용 지정된 데이터베이스 계정에 대 한 클라이언트 Ip의 목록으로 포함 하는 CIDR 형식 toobe hello 집합을 제공 해야 합니다. 이 구성이 적용 되 고 나면이 허용된 목록 외부 컴퓨터에서 발생 한 모든 요청 hello 서버에 의해 차단 됩니다.  IP 기반 액세스 제어 hello에 대 한 흐름을 처리 하는 hello 연결 hello 다이어그램을 다음에 설명 됩니다.

![IP 기반 액세스 제어에 대 한 hello 연결 프로세스를 보여 주는 다이어그램](./media/firewall-support/firewall-support-flow.png)

## <a name="connections-from-cloud-services"></a>클라우드 서비스에서 연결
Azure에서 클라우드 서비스는 Azure Cosmos DB를 사용하여 중간 계층 서비스 논리를 호스팅하는 매우 일반적인 방법입니다. 클라우드 서비스에서 Azure Cosmos DB 데이터베이스 계정 액세스 tooan tooenable, hello hello 클라우드 서비스의 공용 IP 주소 추가 toohello 허용 하 여 Azure Cosmos DB 데이터베이스 계정에 연결 된 IP 주소의 목록 이어야 합니다 [구성 IP 액세스 제어 정책 hello](#configure-ip-policy)합니다.  이렇게 하면 클라우드 서비스의 모든 역할 인스턴스에 액세스 tooyour Azure Cosmos DB 데이터베이스 계정. 다음 스크린 샷에서 hello와 같이 hello Azure 포털에서에서 클라우드 서비스에 대 한 IP 주소를 검색할 수 있습니다.

![Hello hello Azure 포털에에서 표시 되는 클라우드 서비스에 대 한 공용 IP 주소를 보여 주는 스크린샷](./media/firewall-support/public-ip-addresses.png)

이러한 새 인스턴스에 액세스 toohello Azure Cosmos DB 데이터베이스 계정을 자동으로 부여 됩니다 추가 역할 인스턴스를 추가 하 여 클라우드 서비스를 확장할 때 동일한 클라우드 서비스의 hello 속하므로 합니다.

## <a name="connections-from-virtual-machines"></a>가상 컴퓨터에서 연결
[가상 컴퓨터](https://azure.microsoft.com/services/virtual-machines/) 또는 [가상 컴퓨터 크기 집합](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) 사용된 toohost Azure Cosmos DB를 사용 하 여 중간 계층 서비스 일 수도 있습니다.  hello 허용 하 여 Azure Cosmos DB 데이터베이스 계정에 대 한 IP 주소 중 하나로 tooconfigure hello Azure Cosmos DB 데이터베이스 계정 tooallow 액세스, 가상 컴퓨터, 가상 컴퓨터 및/또는 가상 컴퓨터 크기 집합의 공용 IP 주소를 구성 해야 합니다. [hello IP 액세스 제어 정책 구성](#configure-ip-policy)합니다. 다음 스크린 샷에서 hello와 같이 hello Azure 포털에서에서 가상 컴퓨터에 대 한 IP 주소를 검색할 수 있습니다.

![Hello Azure 포털에에서 표시 되는 가상 컴퓨터에 대 한 공용 IP 주소를 보여 주는 스크린샷](./media/firewall-support/public-ip-addresses-dns.png)

추가 가상 컴퓨터 인스턴스 toohello 그룹을 추가할 때 액세스 tooyour Azure Cosmos DB 데이터베이스 계정은 자동으로 제공 됩니다.

## <a name="connections-from-hello-internet"></a>연결 hello 인터넷
때 액세스는 Azure Cosmos DB 데이터베이스 컴퓨터에서 계정에 인터넷 hello, hello 클라이언트 IP 주소 또는 hello 컴퓨터의 IP 주소 범위 해야 추가 toohello hello Azure Cosmos DB 데이터베이스 계정에 대 한 IP 주소 목록을 허용 합니다. 

## <a id="configure-ip-policy"></a>Hello IP 액세스 제어 정책 구성
hello IP 액세스 제어 정책 hello Azure 포털에서에서 설정할 수 있습니다 또는 통해 프로그래밍 방식으로 [Azure CLI](cli-samples.md), [Azure Powershell](powershell-samples.md), 또는 hello [REST API](/rest/api/documentdb/) hello를업데이트하여`ipRangeFilter` 속성입니다. IP 주소/범위는 쉼표로 구분하며 공백을 포함해서는 안 됩니다. 예: "13.91.6.132,13.91.6.1/24". 이러한 메서드를 통해 데이터베이스 계정을 업데이트할 때 수 있는지 toopopulate 모든 hello 속성 tooprevent toodefault 설정을 다시 설정 합니다.

> [!NOTE]
> Azure Cosmos DB 데이터베이스 계정에 대 한 IP 액세스 제어 정책을 활성화 하 여 모든 액세스 tooyour hello 구성 된 외부 컴퓨터에서 Azure Cosmos DB 데이터베이스 계정 차단 된 IP 주소 범위 목록이 허용 합니다. 이 모델을 통해 hello 데이터 평면 작업 hello 포털에서 검색 됩니다 액세스 제어의 차단 된 tooensure hello 무결성.

toosimplify 개발 hello Azure 포털을 사용 하면를 식별 하 고 컴퓨터를 실행 중인 응용 프로그램 hello Azure Cosmos DB 계정에 액세스할 수 있도록 허용 목록에 클라이언트 컴퓨터 toohello의 hello IP를 추가 합니다. Note hello 포털에 표시 된 대로 hello 클라이언트 IP 주소를 여기도 검색 합니다. Hello 클라이언트 IP 주소, 컴퓨터의 수도 있지만 네트워크 게이트웨이의 IP 주소 hello 일 수도 있습니다. Tooremove를 잊지 마십시오 진행 중인 tooproduction 이전 합니다.

hello Azure 포털에서에서 tooset hello IP 액세스 제어 정책 toohello Azure Cosmos DB 계정 블레이드를 탐색, 클릭 **방화벽** hello 탐색 메뉴를 클릭 한 다음 **ON** 

![Tooopen hello Azure 포털에서에서 방화벽 블레이드 hello 하는 방법을 보여 주는 스크린샷](./media/firewall-support/azure-portal-firewall.png)

Hello 새 창에서 지정 하는지 여부를 hello Azure 포털 수 hello 계정에 액세스 하 고를 적절 하 게 다른 주소 및 범위의 추가 입력 한 다음 클릭 **저장**합니다.  

> [!NOTE]
> IP 액세스 제어 정책을 사용 하도록 설정 하면 Azure 포털 toomaintain 액세스 hello tooadd hello IP 주소가 필요 합니다. hello 포털 IP 주소는 있습니다.
> |지역|IP 주소|
> |------|----------|
> |아래 지정된 지역을 제외한 모든 지역| 104.42.195.92|
> |독일|51.4.229.218|
> |중국|139.217.8.252|
> |미국 정부 애리조나|52.244.48.71|
>

![방법을 보여 주는 스크린샷 hello Azure 포털의에서 tooconfigure 방화벽 설정](./media/firewall-support/azure-portal-firewall-configure.png)

## <a name="troubleshooting-hello-ip-access-control-policy"></a>Hello IP 액세스 제어 정책 문제 해결
### <a name="portal-operations"></a>포털 작업
Azure Cosmos DB 데이터베이스 계정에 대 한 IP 액세스 제어 정책을 활성화 하 여 모든 액세스 tooyour hello 구성 된 외부 컴퓨터에서 Azure Cosmos DB 데이터베이스 계정 차단 된 IP 주소 범위 목록이 허용 합니다. 따라서 컬렉션 및 문서를 쿼리 화 tooenable 포털 데이터 평면 작업을 하려는 경우 필요한 tooexplicitly hello를 사용 하 여 Azure 포털 액세스를 허용 **방화벽** 블레이드 hello 포털에서입니다. 

![방법을 보여 주는 스크린샷 tooenable 액세스 toohello Azure 포털](./media/firewall-support/azure-portal-access-firewall.png)

### <a name="sdk--rest-api"></a>SDK 및 Rest API
보안상의 이유로 hello 허용 목록에 없는 컴퓨터에서 SDK 또는 REST API를 통해 액세스 일반적인 404 찾을 수 없음 응답 없는 추가 정보가 반환 됩니다. Hello IP 허용 목록 Azure Cosmos DB 데이터베이스 계정 tooensure hello 올바른 정책 구성에 대해 구성 된는 적용 된 tooyour Azure Cosmos DB 데이터베이스 계정을 확인 하십시오.

## <a name="next-steps"></a>다음 단계
네트워크 관련 성능 팁에 대한 정보는 [성능 팁](performance-tips.md)을 참조하세요.

