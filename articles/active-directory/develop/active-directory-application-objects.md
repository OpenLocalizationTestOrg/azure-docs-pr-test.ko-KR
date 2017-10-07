---
title: "aaaAzure Active Directory 응용 프로그램 및 서비스 주체 개체 | Microsoft Docs"
description: "응용 프로그램 및 Azure Active Directory에 서비스 사용자 개체 간의 hello 관계에 대 한 내용"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Azure Active Directory(Azure AD)의 응용 프로그램 및 서비스 주체 개체
경우에 따라 hello Azure AD의 hello 컨텍스트에서 사용할 경우 잘못 이해할 수 있습니다 "application" hello 용어의 의미 합니다. 이 문서의 hello 목표는 toomake 등록 및에 대 한 동의 보여 줍니다와 Azure AD 응용 프로그램 통합의 개념과 구체적인 측면을 설명 하 여 명확 하 게 하는 [다중 테 넌 트 응용 프로그램](active-directory-dev-glossary.md#multi-tenant-application)합니다.

## <a name="overview"></a>개요
Azure AD와 통합 된 응용 프로그램은 hello 소프트웨어 측면을 벗어나는 하 합니다. "응용 프로그램" 자주 사용 개념적 용어로 Azure AD 등록을 역할 런타임 시 "대화" 인증/권한 부여에도 toonot만 hello hello 응용 프로그램 소프트웨어를 참조 합니다. 정의 따라 응용 프로그램에서 작동할 수 있습니다는 [클라이언트](active-directory-dev-glossary.md#client-application) 역할 (리소스 사용)는 [리소스 서버](active-directory-dev-glossary.md#resource-server) (노출을 Api tooclients), 역할 또는 둘 다도 합니다. hello 대화 프로토콜에 의해 정의 됩니다는 [OAuth 2.0 권한 부여 흐름](active-directory-dev-glossary.md#authorization-grant), 데이터 수 있도록 허용 hello 클라이언트/리소스 tooaccess/보호 된 리소스의 각각. 이제 수준 아래 인 돌아가겠습니다 고 hello Azure AD 응용 프로그램 모델 디자인 타임 및 런타임에 응용 프로그램을 나타내는 하는 방법을 참조 합니다. 

## <a name="application-registration"></a>응용 프로그램 등록
Hello에 Azure AD 응용 프로그램을 등록 하면 [Azure 포털][AZURE-Portal], 두 개체는 Azure AD 테 넌 트에서 생성: 응용 프로그램 개체 및 서비스 사용자 개체입니다.

#### <a name="application-object"></a>응용 프로그램 개체
Azure AD 응용 프로그램 hello 응용 프로그램의 "홈" 테 넌 트로 알려진 하나 및 hello 응용 프로그램 등록 된 hello Azure AD 테 넌 트에 있는 응용 프로그램 개체만으로 정의 됩니다. Azure AD 그래프 hello [응용 프로그램 엔터티] [ AAD-Graph-App-Entity] 응용 프로그램 개체 속성에 대 한 hello 스키마를 정의 합니다. 

#### <a name="service-principal-object"></a>서비스 주체 개체
hello 서비스 사용자 개체에서 런타임에 보안 주체 toorepresent hello 응용 프로그램에 대 한 hello 기반을 제공 하는 특정 테 넌 트에서 hello 정책 및 응용 프로그램의 사용에 대 한 사용 권한을 정의 합니다. Azure AD 그래프 hello [ServicePrincipal 엔터티] [ AAD-Graph-Sp-Entity] 서비스 사용자 개체의 속성에 대 한 hello 스키마를 정의 합니다. 

#### <a name="application-and-service-principal-relationship"></a>응용 프로그램 및 서비스 주체 관계
Hello로 hello 응용 프로그램 개체는 것이 좋습니다 *글로벌* hello로 모든 테 넌 트 및 hello 서비스 사용자에서 사용 하기 위해 응용 프로그램의 표현을 *로컬* 특정에서 사용 하기 위해 표현 테 넌 트입니다. hello 응용 프로그램 개체는 해당 역할을 hello는 공통에서 서식 파일 및 기본 속성은 *파생* 를 해당 서비스 보안 주체 개체를 만드는 데 사용 합니다. 1:1 관계가 hello 소프트웨어 응용 프로그램 및 서비스는 해당 주 개체와 다 관계에 따라서 응용 프로그램 개체에 있습니다.

Hello 응용 프로그램 사용 되며 tooestablish 로그인에 대 한 id를 사용 하는 경우 및/또는 액세스 tooresources hello 테 넌 트로 보호 되 고 각 테 넌 트에 서비스 사용자를 만들어야 합니다. 단일 테넌트 응용 프로그램에는 해당 홈 테넌트에 하나의 서비스 주체만 있으며 일반적으로 응용 프로그램 등록 중에 생성하고 동의합니다. 다중 테 넌 트 웹 응용 프로그램/API에서는 갖게 각 테 넌 트에서 만든 서비스 사용자에서 해당 테 넌 트 사용자가 tooits 사용 동의 하는 위치입니다.  

> [!NOTE]
> Tooyour 응용 프로그램 개체를 수행한 모든 변경 사항은 hello 응용 프로그램의 홈 테 넌 트에만 (hello 테 넌 트 등록 된)의 서비스 사용자 개체에도 반영 됩니다. 다중 테 넌 트 응용 프로그램에 대 한 변경 toohello 응용 프로그램 개체에에서 반영 되지 않으며 모든 소비자 테 넌 트의 서비스 사용자 개체 hello 액세스 hello를 통해 제거 될 때까지 [응용 프로그램 액세스 패널로](https://myapps.microsoft.com) 다시 부여 합니다.
><br>  
> 또한 기본적으로 네이티브 응용 프로그램이 다중 테넌트로 등록됩니다.
> 
> 

## <a name="example"></a>예제
hello 다음 보여 주는 다이어그램 응용 프로그램의 응용 프로그램 개체와 해당 서비스 보안 주체 개체 샘플 다중 테 넌 트 응용 프로그램의 hello 컨텍스트에서 호출 hello 관계 **HR 앱**합니다. 이 시나리오에는 세 가지 Azure AD 테넌트가 있습니다. 

* **Adatum** -hello hello를 개발 하는 hello 회사에서 사용 하는 테 넌 트 **HR 앱**
* **Contoso** -hello hello hello의 소비자를 Contoso 조직에서 사용 하는 테 넌 트 **HR 앱**
* **Fabrikam** -hello hello도 hello를 사용 하는 Fabrikam 조직에서 사용 하는 테 넌 트 **HR 앱**

![응용 프로그램 개체 및 서비스 주체 개체 간의 관계](./media/active-directory-application-objects/application-objects-relationship.png)

Hello 이전 다이어그램에서 단계 1 hello hello 응용 프로그램의 홈 테 넌 트의 hello 응용 프로그램 및 서비스 보안 주체 개체를 만드는 과정은 합니다.

2 단계에서에서 Contoso 및 Fabrikam 관리자 동의 완료할 때 서비스 사용자 개체에 만들어집니다 회사의 Azure AD 테 넌 트 및 할당 된 hello 사용 권한을 부여 하는 hello 관리자. 또한 해당 hello HR 앱 각각의 사용에 대 한 사용자가 구성 하 고 설계 tooallow 동의 수 note 합니다.

3 단계 hello HR 응용 프로그램 (예: Contoso 및 Fabrikam) 각의 hello 소비자 테 넌 트가 자체 서비스 사용자 개체를 갖고 있습니다. 각 사용을 하 여 해당 관리자에 게 사용 권한을 승인 hello에 준하여 런타임에 hello 응용 프로그램의 인스턴스를 나타냅니다.

## <a name="next-steps"></a>다음 단계
응용 프로그램의 응용 프로그램 개체를 통해 액세스할 수 hello Azure AD Graph API hello [Azure 포털의] [ AZURE-Portal] 응용 프로그램 매니페스트 편집기 또는 [Azure AD PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0)의 OData에 표시 된 대로, [응용 프로그램 엔터티][AAD-Graph-App-Entity]합니다.

응용 프로그램의 서비스 사용자 개체 hello Azure AD Graph API 통해 액세스할 수 또는 [Azure AD PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0)의 OData에 표시 된 대로, [ServicePrincipal 엔터티] [ AAD-Graph-Sp-Entity].

hello [Azure AD 그래프 탐색기](https://graphexplorer.azurewebsites.net/) hello 응용 프로그램 및 서비스 보안 주체 개체를 모두 쿼리 하는 데 유용 합니다.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
