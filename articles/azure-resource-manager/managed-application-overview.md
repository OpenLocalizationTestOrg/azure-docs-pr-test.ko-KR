---
title: "Azure의 aaaOverview 관리 응용 프로그램 | Microsoft Docs"
description: "Azure 용 hello 개념을 설명 합니다. 응용 프로그램 관리"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 2fd1844a442515f4492c890c9798073475a66f88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-overview"></a>Azure 관리되는 응용 프로그램 개요

Azure를 사용 하는 공급 업체 솔루션 toocustomers hello 전 세계를 제공할 수 있습니다. Azure Marketplace는 자사 및 타사 공급업체에서 제공하는 수백 가지의 복잡한 다중 리소스 템플릿으로 구성된 갤러리입니다. 고객은 몇 분 이내로 PaaS(Platform as a Service) 및 SaaS(Software as a Service) 응용 프로그램을 사용하여 배포하고 시작할 수 있습니다. 

Hello 마켓플레이스를 매우 편리를 제공 하지만 고객 tooquickly 배포는 제품, hello 고객은 유지 관리 하 고 hello 솔루션을 업데이트 하는 일을 담당 합니다. 초과 hello 가상 컴퓨터 이미지 요금 청구서 주소, 공급 업체 응용 프로그램의 hello 사용에 대 한 고객 충전 수 없습니다. 또한 공급 업체는 고객이 중요한 응용 프로그램 리소스를 수정하는 것을 방지할 수 없습니다. 또한 공급 업체 응용 프로그램을 구성 하는 액세스 toointellectual 속성을 차단할 수 없습니다. Azure 관리되는 응용 프로그램은 이러한 문제를 해결할 수 있는 솔루션을 제공합니다. 

관리 되는 응용 프로그램은 hello Marketplace와의 비슷한 tooa 솔루션 템플릿입니다. 관리 되는 응용 프로그램에서는 hello 리소스가 hello 공급 업체에서 관리 되는 프로 비전 된 tooa 리소스 그룹입니다. 리소스 그룹 hello hello 고객의 구독에 있는 않으며 hello 공급 업체의 테 넌 트의 id에 대 한 액세스 toohello 리소스 그룹입니다.

## <a name="advantages-of-managed-applications"></a>관리되는 응용 프로그램의 이점

서비스 공급자 (Msp) Isv, 관리 되는 중앙 회사 IT 팀 hello 마켓플레이스를 통해 관리 되는 응용 프로그램 toodeliver 솔루션을 사용 하거나 서비스 카탈로그 hello 수 있습니다. Toomaintain 없는 고객의 구독에 관리 되는 이러한 응용 프로그램을 배포 하지만, 업데이트 또는 서비스입니다. 공급 업체를 관리 하 고 hello 응용 프로그램을 지원 하기 때문에 고객 없는 toodevelop 응용 프로그램별 도메인 기술 toomanage 이러한 응용 프로그램입니다. 고객은 hello 응용 프로그램의 문제 진단 및 문제 해결에 대 한 hello 필요 tooworry 없이 응용 프로그램 업데이트를 자동으로 가져온 수 있습니다.

관리 되는 응용 프로그램 공급 업체 및 공급자에 대 한 채널 toosell 인프라와 hello 마켓플레이스를 통해 소프트웨어를 만듭니다. 관리 되는 응용 프로그램 제공 방법 tooattach 서비스 및 운영 지원 tooAzure 고객 합니다. Hello Azure 청구 시스템을 사용 하 여 공급 업체에서 고객 요금을 청구할 수 있습니다. 배포 된 응용 프로그램의 템플릿 toomanage hello 수명 주기를 사용할 수 있습니다. 이러한 솔루션 독립적 이면 서 sealed toohello 고객 되므로 공급 업체는 고품질 서비스를 제공할 수 있습니다. 이 방법은 PaaS 및 SaaS 공급 업체를 활용합니다. 회사 중앙 플랫폼 팀 및 시스템 통합자 (SIs)에 도움이 toopackage 원하는 사람과 재판매 해결 합니다.

## <a name="managed-application-types"></a>관리되는 응용 프로그램 종류
Azure 관리되는 응용 프로그램은 서비스 카탈로그와 Marketplace라는 두 가지 종류로 제공됩니다.
 
### <a name="service-catalog"></a>서비스 카탈로그  

서비스 카탈로그 hello 고객 조직에서 사용자가 사용 하는 Azure toobe에 대 한 승인 된 솔루션의 카탈로그를 만들 수 있습니다. 이러한 솔루션 카탈로그를 유지 관리하는 것은 기업의 중앙 IT 팀에 도움이 됩니다. 조직에 대 한 솔루션을 제공 하는 동안 특정 조직 표준 준수 카탈로그 tooensure hello를 사용할 수 있습니다. 이러한 응용 프로그램을 제어, 업데이트 및 유지 관리할 수 있습니다. 직원 צ ְ ײ hello 카탈로그 tooeasily hello 다양 한 권장 및 IT 부서에서 승인 되는 응용 프로그램을 검색 합니다. 고객은 자신이 만든 hello 서비스 카탈로그를 관리 하는 응용 프로그램을 표시 합니다. 또한 hello 관리 응용 프로그램을 자신의 조직 공유에는 다른 사람이 표시 됩니다.
 
서비스 카탈로그 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시](managed-application-publishing.md)를 참조하세요.
 
서비스 카탈로그 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 사용](managed-application-consumption.md)을 참조하세요.
 
### <a name="marketplace"></a>마켓플레이스

관리 되는 응용 프로그램은 hello Azure 포털에에서 hello 마켓플레이스를 통해 사용할 수 있습니다. Hello 공급 업체가 이러한 응용 프로그램을 게시 한 후에 내부 또는 조직 tooconsume 외부 모든 사용자에 대해 사용할 수 있습니다. 이 접근 방식 Msp, Isv 및 SIs 제공할 수 자신의 솔루션 tooall Azure 고객 합니다. 고객은 hello 필요 tooinvest 이해 하 고 hello 솔루션 유지 관리 하지 않고 이러한 복잡 한 솔루션을 사용 하 여 hello 혜택을 받을입니다. 

현재는 게시자가 관리되는 응용 프로그램 또는 관리되지 않는 솔루션 템플릿으로 제품을 사용할 수 있도록 합니다. 관리 되는 응용 프로그램을 게시 하는 주요 구성 요소 hello hello 템플릿 파일 및 hello UI 정의 파일에 포함 됩니다. hello 템플릿 파일에 프로 비전 되는 hello 리소스에 설명 합니다. hello UI 정의 파일 hello 필수 이러한 리소스를 프로 비전에 대 한 입력 hello 포털에서 표시 하는 방법을 설명 합니다. hello 파일을.zip 파일로 패키지 되 고 hello 게시 포털을 통해 업로드 해야 합니다.
 
관리 되는 응용 프로그램 toohello 마켓플레이스를 게시 하는 방법에 대 한 정보를 참조 하십시오. [Azure 마켓플레이스 hello에 대 한 응용 프로그램 관리](managed-application-author-marketplace.md)합니다.

Hello 시장에서에서 관리 되는 응용 프로그램을 사용 하는 방법에 대 한 정보를 참조 하십시오. [사용할 Azure 관리 응용 프로그램 마켓플레이스 hello에](managed-application-consume-marketplace.md)합니다.

## <a name="key-concepts"></a>주요 개념

### <a name="managed-resource-group"></a>관리되는 리소스 그룹
hello 관리 되는 리소스 그룹은 Azure을 hello 모든 hello 서식 파일에 프로 비전 되는 리소스가 생성 합니다. 예를 들어 저장소 계정을 사용 하는 toocreate hello 어플라이언스를 사용 하는 경우에이 리소스 그룹 hello 저장소 계정 리소스를 포함 합니다. Hello 기기 리소스를 포함 하 고 하지 않습니다.

### <a name="appliance-package"></a>어플라이언스 패키지
hello 게시자 hello 템플릿 파일과 hello createUIDefinition 파일을 포함 하는 패키지를 만듭니다. 특히, hello를 다음 파일이 포함 되어 있습니다.

- **applianceMainTemplate.json**:이 템플릿 파일 hello 기기에서 프로 비전 되는 모든 hello 리소스를 정의 합니다. 이 파일은 toocreate 리소스 사용에 일반 템플릿 파일입니다.

- **MainTemplate.json**:이 템플릿 파일 hello 기기 리소스 (Microsoft.Solutions/appliances)를 정의 합니다. 이 리소스에 정의되는 하나의 주요 속성은 ManagedResourceGroupId입니다. 이 속성에 있는 리소스 그룹을 사용 하는 toohost hello 실제 리소스를 applianceMainTemplate.json에 정의 된 나타냅니다.

- **applianceCreateUIDefinition.json**:이 파일에서는 hello 필요한 hello 서식 파일에 정의 된 hello 매개 변수에 대 한 UI를 렌더링 하는 방식을 설명 합니다.

### <a name="authorization"></a>권한 부여
hello 게시자 hello 공급 업체 toomanage hello 리소스 hello 고객을 대신 하는 데 필요한 hello 사용 권한을 지정 해야 합니다. 이 사용 권한은 toohello 관리 되는 리소스 그룹을 적용합니다. Hello 다음 값을 설정 합니다.

- **PrincipalID**: hello hello 사용자, 그룹 또는 toogrant 액세스 toohello 관리 되는 리소스 그룹을 사용 하는 응용 프로그램의 Azure Active Directory (Azure AD) 식별자입니다. 이 식별자는 toohello 게시자의 테 넌 트를 속해 있습니다.

- **RoleDefinitionID**: hello hello 할당 된 역할 toohello 앞에 보안 주체 ID의 Azure AD 식별자 Hello hello 게시자의 테 넌 트의 기본 제공 역할 기반 액세스 제어 역할 중 하나일 수 있습니다. 자세한 내용은 [Azure 역할 기반 액세스 제어의 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

* 게시는 관리 되는 응용 프로그램 toohello Marketplace에 대 한 정보를 참조 하십시오. [Azure 마켓플레이스 hello에 대 한 응용 프로그램 관리](managed-application-author-marketplace.md)합니다.
* Hello 시장에서에서 관리 되는 응용 프로그램을 사용 하는 방법에 대 한 정보를 참조 하십시오. [사용할 Azure 관리 응용 프로그램 마켓플레이스 hello에](managed-application-consume-marketplace.md)합니다.
* 서비스 카탈로그 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시](managed-application-publishing.md)를 참조하세요.
* 서비스 카탈로그 관리되는 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [서비스 카탈로그 관리되는 응용 프로그램 사용](managed-application-consumption.md)을 참조하세요.
* toocreate UI 정의 파일을 참조 하세요. [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
