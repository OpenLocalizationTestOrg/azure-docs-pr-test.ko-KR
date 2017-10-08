---
title: "aaaTechnical 마켓플레이스 hello에 대 한 데이터 서비스를 만들기 위한 필수 조건 | Microsoft Docs"
description: "데이터 서비스 toodeploy를 만들기 위한 hello 요구 사항을 이해 하 고 hello Azure Marketplace에 판매 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>Azure 마켓플레이스 hello에 대 한 데이터 서비스를 만들기 위한 필수 구성 요소 기술 제공
> [!IMPORTANT]
> **현재는 새 데이터 서비스 게시자 등록을 더 이상 받지 않고 있습니다. 따라서 새 데이터 서비스 등재 승인을 받을 수 없습니다.** SaaS 비즈니스 응용 프로그램의 경우 원하는 toopublish AppSource에 자세한 정보를 찾을 수 [여기](https://appsource.microsoft.com/partners)합니다. IaaS 응용 프로그램 또는 서비스 개발자 경우는 Azure 마켓플레이스에서 toopublish 같은 자세한 정보를 찾을 수 [여기](https://azure.microsoft.com/marketplace/programs/certified/)합니다.
> 
> 

Hello 프로세스 시작 하기 전에 철저 하 게 읽고 각 단계도 수행 하는 위치와 이유를 이해 합니다. 가능한 한 있습니다 해야 회사 정보 및 기타 데이터를 준비, 필요한 도구를 다운로드 및/또는 hello 제안 만들기 프로세스를 시작 하기 전에 기술 구성 요소를 만들어야 합니다.

다음 항목 hello 프로세스를 시작 하기 전에 hello가 있어야 합니다.

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>데이터 서비스 제안을 기술은 사용된 toopublish 수 있는지에 결정을 내릴
게시자는 Azure 마켓플레이스에 데이터 서비스를 게시할 때 여러 가지 기술 중 하나를 결정할 수 있습니다. hello 주요 기술 지원 되는 아래에서 설명 합니다. 기술은 사용 되는 toopublish hello 데이터 서비스에 관계 없이, hello 통해 hello 데이터를 사용 하는 hello 최종 사용자 **OData 피드** Azure 마켓플레이스 서비스에서 노출 합니다. OData 서비스에 대한 모든 정보는 [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>SQL Azure 데이터베이스
SQL Azure에 데이터 집합을 준비하는 것은 게시자의 책임입니다. Toosubscribe tooAzure 해야 데이터베이스의 적절 한 크기를 프로 비전 하 고 SQL Azure DB로 데이터를 업로드 합니다. 게시자 이기도 책임 tookeep 자신의 데이터를 항상 최신 상태입니다. 찾을 수 tooAzure 서비스를 구독 하는 방법에 대 한 자세한 내용은 [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

SQL Azure로 hello 데이터를 이동할 때는 hello Azure 마켓플레이스 테이블 및 뷰를 노출할 수 있습니다. 테이블/뷰 및 열을 노출 된 toohello 최종 사용자는 hello 게시자 지정할 수 있습니다. 추가 hello 콘텐츠 공급자 hello 최종 사용자는 열을 쿼리할 수 있습니다 및 알림을 hello 페이로드에 정보만 반환 됩니다 지정할 수도 있습니다. 이렇게 하면 높은 수준의 유연성에 대 한 hello 데이터베이스의에서 데이터를 노출 해야 합니다. 쿼리할 수 있는 열이 하나 이상의 데이터베이스 인덱스 뒷받침 되며 toobe가 필요 합니다.

## <a name="rest-based-web-service"></a>REST 기반 웹 서비스
지원되는 프로토콜: **HTTPS만**

기존 REST 기반 서비스는 hello Azure 마켓플레이스를 통해 노출 될 수 있습니다. 필요한 Azure 마켓플레이스 서비스 hello를 OData 피드로 hello 데이터 집합은 항상 노출 된 toohello 최종 사용자 때문에 toobe 수 toomap hello 서비스 tooa OData 기반 서비스입니다. hello REST 끝점을 기반으로 않도록 toodo HTTP 매개 변수로 tooexpose 모든 매개 변수가 필요 합니다.

hello 페이로드는 ATOM 응답에 매핑할 수 있는 형태로 toobe가 필요 합니다. 따라서 hello 서비스의 hello 응답 XML 형식으로 toobe 하며만 (예: 레코드 집합) hello 페이로드 값이 포함 된 하나의 반복 되는 요소를 포함할 수 있습니다. hello Azure 마켓플레이스 서비스는 hello 반복 hello 및 ATOM 페이로드 값 노드 toohello 항목 노드 hello 항목 노드 내에 있는 노드 속성에 매핑됩니다.

권한 부여 정보 (예: API 키와 인증 토큰 등)는 기본 인증도 지원 되며 hello HTTP 헤더 (키-값 쌍) – 또는 HTTP 매개 변수로 제공 toobe가 필요 합니다. 유효한 키 toobe 제공 되어야 하며 해당 키를 통해 Azure Marketplace를 통해 모든 요청 내용이 합니다. 사용자 모니터링과 요금 청구 hello Azure 마켓플레이스 계층에서 발생 합니다.

Hello 서비스에서 반환 된 오류는 HTTP 상태 코드에 매핑된 toobe가 필요 합니다. Hello 서비스 hello 오류가 포함 된 XML을 반환 하는 경우 이러한 하려고 합니다 toobe hello Azure 마켓플레이스 서비스 tooHTTP 상태 코드로 매핑됩니다.

## <a name="soap-based-web-services"></a>SOAP 기반 웹 서비스
프로토콜: **HTTPS만**

hello 요구 사항은 hello REST 기반 서비스 섹션에서와 같이 hello 동일 합니다. hello 유일한 차이점은 Azure 마켓플레이스를 통해 모든 요청에 서비스 toohello 게시자의 게시 되는 XML 본문에서 매개 변수를 제공할 수도 있습니다. 즉, HTTP 매개 변수 hello 사용자 제공 hello 프런트 엔드에 hello 요청 toohello 콘텐츠 공급자의 웹 서비스와 함께 게시 되는 XML 문서의 XML 요소로 변환 되 고 됩니다.

## <a name="odata-based-web-services"></a>OData 기반 웹 서비스
프로토콜: **HTTPS만**

OData 서비스 tooAzure 마켓플레이스로 데이터를 노출할 수 있습니다. hello 시스템은 지속적인 toopass hello 서비스를 통해를 hello Azure 마켓플레이스 서비스 루트 – Azure Marketplace를 통해 모든 후속 호출은 이동 tooensure hello 서비스의 hello 루트 바꿉니다.

OData 서비스는 hello 백 엔드에서 데이터베이스에 대해 toogo만 않아도 됩니다. OData는 모든 종류의 저장소 또는 비즈니스 논리 toodrive hello 서비스를 지원합니다.

## <a name="next-steps"></a>다음 단계
Hello에 대 한 필수 정보를 검토 하 고 hello 필요한 작업 완료 진행 하려면 hello에 설명된 된 hello로 데이터 서비스 제공 만들기로 [데이터 서비스에 대 한 게시 가이드](marketplace-publishing-data-service-creation.md)합니다.

각 단계를 게시 하는 hello에 대 한 전반적인 프로세스 tooreview hello 및 hello 해당 기사 싶으면, hello 문서를 참조 하십시오 또는 [시작: 어떻게 toopublish 제안 toohello Azure 마켓플레이스](marketplace-publishing-getting-started.md)합니다.

[link-acct]:marketplace-publishing-accounts-creation-registration.md
