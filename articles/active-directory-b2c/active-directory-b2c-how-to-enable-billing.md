---
title: "Azure 구독 tooAzure AD B2C aaaHow tooLink | Microsoft Docs"
description: "Azure AD B2C 테 넌 트에 대 한 tooenable 청구 단계별 가이드를 Azure 구독에 있습니다."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>Azure 구독 tooan Azure B2C 테 넌 트 toopay 사용 요금에 대 한 연결

Azure Active Directory B2C (또는 Azure AD B2C)에 대 한 지속적인 사용 요금 청구 tooan Azure 구독 됩니다. Hello 테 넌 트 관리자 tooexplicitly 링크 hello Azure AD B2C 테 넌 트 tooan 자체 hello B2C 테 넌 트를 만든 후 Azure 구독에 대 한 필요는.  이 링크는 Azure AD "B2C 테 넌 트"를 만들어 구현할 hello 대상 Azure 구독에에서 리소스입니다. 많은 B2C 테 넌 트가 다른 Azure 리소스 (예: Vm, 데이터 저장소, LogicApps)와 함께 연결 된 tooa 단일 Azure 구독 수 있습니다.


> [!IMPORTANT]
> 사용 대금 청구 및 B2C hello 페이지 다음에 가격 책정에 대 한 최신 정보를 hello: [Azure AD B2C 가격 책정](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>1단계 - Azure AD B2C 테넌트 만들기
먼저 B2C 테넌트 만들기를 완료해야 합니다. 이미 대상 B2C 테넌트를 만든 경우에는 이 단계를 건너뜁니다. [Azure AD B2C 시작](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>2 단계-Azure AD 테 넌 트 Azure 구독을 보여 주는 hello에 Azure 포털 열기
Toohello 이동 [Azure 포털](https://portal.azure.com)합니다. Azure AD 테 넌 트 hello toouse 원하는 Azure 구독을 보여 주는 toohello를 전환 합니다. 이 Azure AD 테 넌 트는 hello B2C 테 넌 트와에서 다릅니다. Hello Azure 포털 내에서 hello hello 대시보드 tooselect hello Azure AD 테 넌 트의 오른쪽 위에 hello 계정 이름을 클릭 합니다. Azure 구독에 필요한 tooproceed입니다. [Azure 구독 가져오기](https://account.windowsazure.com/signup?showCatalog=True)

![Azure AD 테 넌 트 tooyour 전환](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>3단계 - Azure Marketplace에서 B2C 테넌트 리소스 만들기
마켓플레이스 hello hello 대시보드의 맨 왼쪽된 위에 있는 hello 마켓플레이스 아이콘을 클릭 하거나 hello 녹색 "+"를 선택 하 여 엽니다.  Azure Active Directory B2C를 검색하고 선택합니다. 만들기를 선택합니다.

![Marketplace 선택](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![AD B2C 검색](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

hello Azure AD B2C 리소스 만들기 대화 상자에서는 hello 매개 변수 뒤:

1. Azure AD B2C 테 넌 트-hello 드롭다운에서 Azure AD B2C 테 넌 트를 선택 합니다.  적격 Azure AD B2C 테넌트만 표시됩니다.  적격 B2C 테 넌 트에는 다음이 조건을 충족: hello, hello B2C 테 넌 트의 전역 관리자가 아니며 hello B2C 테 넌 트에 현재 연결된 tooan Azure 구독

2. Azure AD B2C 리소스 이름-은 hello B2C 테 넌 트의 미리 선택 된 toomatch hello 도메인 이름

3. 구독 - 관리자이거나 공동 관리자인 활성 Azure 구독입니다.  여러 Azure AD B2C 테 넌 트 tooone Azure 구독을 추가할 수 있습니다.

4. 리소스 그룹 및 리소스 그룹 위치 - 이 아티팩트를 사용하면 여러 Azure 리소스를 구성할 수 있습니다.  이 선택은 B2C 테넌트 위치, 성능 또는 청구 상태에 영향을 주지 않습니다.

5. 쉬운 액세스 tooyour B2C 테 넌 트 청구 정보 및 hello B2C 테 넌 트 설정에 대 한 toodashboard 고정 ![B2C 리소스 만들기](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>4단계 - B2C 테넌트 리소스 관리(선택 사항)
배포가 완료 되 면 관련 Azure 구독 및는 "B2C 테 넌 트" 리소스를 새 hello 대상 리소스 그룹에 생성 됩니다.  다른 "Azure" 리소스와 함께 추가된 "B2C 테넌트" 유형의 새로운 리소스가 표시됩니다.

![B2C 리소스 만들기](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

수 있는 hello B2C 테 넌 트 리소스를 클릭 하면
- 구독 이름 tooreview 청구 정보를 클릭 합니다. 청구 및 사용을 참조하세요.
- Azure AD B2C 설정 tooopen tooyour B2C 테 넌 트 설정 블레이드에서에서 직접 새 브라우저 탭을 클릭 합니다.
- 지원 요청을 제출합니다.
- 프로그램 B2C 테 넌 트 리소스 tooanother 이동 Azure 구독 또는 리소스 그룹 tooanother 합니다.  사용 요금이 이 선택에 따라 Azure 구독에 부과됩니다.

![B2C 리소스 설정](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>알려진 문제
- B2C 테넌트 삭제. B2C 테 넌 트를 만든 경우 삭제 하 고 다시 사용 하 여 만든 동일한 도메인 이름을 hello도 삭제 하십시오 hello 사용 하 여 hello "연결" 리소스를 다시 만드는 동일한 도메인 이름입니다.  "모든 리소스" 아래에서 리소스를 hello Azure 포털을 통해 hello 구독 테 넌 트의 "연결" 알 수 있습니다.
- 지역별 리소스 위치에 자체적인 제한 적용.  드물지만 사용자가 Azure 리소스 만들기에 대해 지역별 제한을 구축했을 수 있습니다.  이 제한 사항은 Azure 구독 및 B2C 테 넌 트 간의 링크 hello hello 생성이 되지 않을 수 있습니다. toomitigate,이 제한 사항은 완화 하세요.

## <a name="next-steps"></a>다음 단계
각 B2C 테넌트에 대해 이러한 단계가 완료되면 Azure 직접 또는 기업 계약 세부 정보에 따라 비용이 Azure 구독에 청구됩니다.
- Azure 구독을 선택한 상태에서 사용 현황 및 청구 검토
- Hello를 사용 하 여 자세한 날짜별으로 사용 현황 보고서를 검토 [사용 현황 보고 API](active-directory-b2c-reference-usage-reporting-api.md)
