---
title: "hello Azure Active Directory에서에서 엔터프라이즈 응용 프로그램에 대 한 관리를 프로 비전 aaaUser | Microsoft Docs"
description: "Toomanage 사용자 계정 hello Azure Active Directory를 사용 하 여 엔터프라이즈 응용 프로그램에 대 한 프로 비전 방법에 대해 알아봅니다"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: a613f844c8f51e04b92e62b488313a78ab85f7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-user-account-provisioning-for-enterprise-apps-in-hello-azure-portal"></a>Hello Azure 포털에서에서 엔터프라이즈 응용 프로그램에 대 한 프로 비전 하는 사용자 계정 관리
이 문서에서는 설명 방법을 toouse hello [Azure 포털](https://portal.azure.com) toomanage 자동 사용자 계정을 프로 비전 하 고 특히 하는 스토리 hello에서 추가 된 속성을 지원 되는 응용 프로그램에 대 한 프로 비전 해제 "추천"의 범주 hello [Azure Active Directory 응용 프로그램 갤러리](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)합니다. 자동 사용자 계정 프로 비전 및 작동 방식에 대해 자세히 toolearn 참조 [자동화 사용자 프로 비전 및 프로 비전 해제 tooSaaS Azure Active Directory와 응용 프로그램](active-directory-saas-app-provisioning.md)합니다.

## <a name="finding-your-apps-in-hello-portal"></a>Hello 포털에서 앱 찾기
Hello를 사용 하 여 디렉터리 관리자가 디렉터리의에서 single sign-on에 대해 구성 된 모든 응용 프로그램 [Azure Active Directory 응용 프로그램 갤러리](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), 보기 및 hello에서 관리 되는 [Azure 포털](https://portal.azure.com). hello 응용 프로그램에 hello 있습니다 **더 서비스** &gt; **엔터프라이즈 응용 프로그램** hello 포털의 섹션입니다. 엔터프라이즈 앱은 조직 내에서 배포 및 사용되는 앱입니다.

![엔터프라이즈 응용 프로그램 블레이드][0]

선택 hello **모든 응용 프로그램** hello 왼쪽에 링크 hello 갤러리에서 추가 된 응용 프로그램을 포함 하 여 구성 되어 있는 모든 앱의 목록을 표시 합니다. 응용 프로그램을 선택 하면 해당 앱에 대 한 보고서를 볼 수 있습니다 하 고 다양 한 설정 관리할 수 있는 해당 앱에 대 한 hello 리소스 블레이드를 로드 합니다.

사용자 계정에 대 한 설정 선택 하 여 관리할 수 있습니다 **프로 비전** hello 왼쪽에 있습니다.

![응용 프로그램 리소스 블레이드][1]

## <a name="provisioning-modes"></a>프로비전 모드
hello **프로 비전** 블레이드로 시작 하는 **모드** 엔터프라이즈 응용 프로그램에 대 한 지원 되는 어떤 프로 비전 모드를 나타내고 toobe 구성할 수 있도록 하는 메뉴입니다. hello 사용할 수 있는 옵션은 다음과 같습니다.

* **자동** -Azure AD 자동 API 기반 프로 비전 및/또는 사용자 계정 toothis 응용 프로그램의 프로 비전 해제를 지원 하면이 옵션이 나타납니다. 이 모드를 선택 하면 Azure AD tooconnect toohello 응용 프로그램 사용자 관리 API 구성, 계정 매핑 및 Azure AD 간에 사용자 계정을 데이터 흐름 방식을 정의 하는 워크플로 만드는 안내 하는 인터페이스를 표시 하 고 hello 앱과 관리 hello Azure AD 제공 서비스입니다.
* **수동** -Azure AD 사용자 계정 toothis 응용 프로그램의 자동 프로 비전 지원 하지 않는 경우이 옵션이 표시 됩니다. 이 옵션은 hello 사용자 관리 및 프로 비전 기능을 해당 응용 프로그램 (SAML Just-In-Time 프로 비전을 포함할 수 있습니다)에서 제공 하는 외부 프로세스를 사용 하 여 hello 응용 프로그램에 저장 된 사용자 계정 레코드를 관리 해야 하는지을 의미 합니다.

## <a name="configuring-automatic-user-account-provisioning"></a>자동 사용자 계정 프로비전 구성
선택 hello **자동** 옵션 4 개 섹션에서 나누어져 있는 화면을 표시 합니다.

### <a name="admin-credentials"></a>관리자 자격 증명
Azure AD tooconnect toohello 응용 프로그램 사용자 관리 API에 필요한 hello 자격 증명을 입력 하는 위치입니다. 필요한 입력이 hello hello 응용 프로그램에 따라 달라 집니다. toolearn hello 자격 증명 유형 및 특정 응용 프로그램에 대 한 요구 사항에 대 한 참조 hello [해당 특정 응용 프로그램에 대 한 구성 자습서](active-directory-saas-app-provisioning.md#list-of-apps-that-support-automated-user-provisioning)합니다.

선택 hello **연결 테스트** 단추를 사용 하면 Azure AD tooconnect toohello 응용 프로그램을 시도 함으로써 tootest hello 자격 증명의 hello 제공 된 자격 증명을 사용 하 여 앱 프로 비전 합니다.

### <a name="mappings"></a>매핑
이 관리자 보고 하 고 Azure AD 간의 어떤 사용자 특성 흐름을 편집할 수 있는 및 hello 대상 응용 프로그램에 사용자 계정을 프로 비전 되거나 업데이트 되 면 합니다.

Azure AD 사용자 개체와 각 SaaS 앱의 사용자 개체 간의 미리 구성된 매핑 세트가 있습니다. 일부 앱은 그룹이나 연락처 같은 다른 유형의 개체를 관리합니다. Hello 테이블에 이러한 매핑 중 하나를 선택 하면 오른쪽 toohello 여기서은 보기 및 사용자 지정 된 hello 매핑 편집기 나와 있습니다.

![응용 프로그램 리소스 블레이드][2]

지원되는 사용자 지정은 다음과 같습니다.

* 설정 및 hello Azure AD 사용자 개체 toohello SaaS 응용 프로그램의 사용자 개체와 같은 특정 개체에 대 한 매핑을 해제 합니다.
* 특성 흐름 사용자 개체 hello Azure AD 사용자 개체 toohello 앱에서에서 편집 합니다. 특성 매핑에 대한 자세한 내용은 [특성 매핑 유형 이해하기](active-directory-saas-customizing-attribute-mappings.md#understanding-attribute-mapping-types)를 참조하세요.
* Azure AD hello에서 수행 하는 작업을 프로 비전 하는 필터 hello 응용 프로그램을 대상으로 합니다. 완전히-개체를 동기화 하는 Azure AD 대신 수행 하는 hello 동작을 제한할 수 있습니다. 예를 들어 **업데이트**만 선택하면 Azure AD가 응용 프로그램에서 기존 사용자 계정을 업데이트만 하며 새 계정을 만들지는 않습니다. **만들기**만 선택하면 Azure가 새 사용자 계정을 만들기만 하고 기존 계정을 업데이트하지는 않습니다. 이 기능은 toocreate 관리자 계정에 대 한 다른 매핑을 생성 및 업데이트 워크플로 수 있습니다.

### <a name="settings"></a>설정
이 섹션에서는 관리자 toostart 및 중지 hello Azure AD 프로비저닝 서비스로 선택적으로 지우기 hello를 프로 비전 뿐만 아니라 hello 선택한 응용 프로그램에 대 한 캐시 하 고 hello 서비스를 다시 시작 합니다.

Hello를 변경 하 여 hello 서비스를 프로 비전 중에 사용 되 면 hello 응용 프로그램에 대해 처음으로, 활성화 **프로 비전 상태** 너무**에**합니다. 이 인해 프로 비전 서비스 tooperform hello Azure AD 읽어 hello에 할당 된 hello 사용자 초기 동기화 **사용자 및 그룹** 섹션에서 고객을 위해 hello 대상 응용 프로그램을 쿼리하고 다음 hello를 프로 비전을 수행 hello Azure AD에에서 정의 된 작업 **매핑** 섹션. 이 과정에서 서비스를 프로 비전 하는 hello 할당에 대 한 범위에 있지 않도록 된 hello 대상 응용 프로그램 내 계정 관리 되지 않는 작업 프로 비전 해제 하 여 영향을 주지 않으므로 하므로 관리 하는 어떤 사용자 계정에 대 한 캐시 된 데이터를 저장 합니다. 초기 동기화 서비스를 자동으로 프로 비전 하는 hello을 hello 후 10 분 간격으로 사용자 및 그룹 개체를 동기화 합니다.

변경 hello **프로 비전 상태** 너무**오프** 일시 중지 하면 hello 제공 서비스입니다. 이 상태에서는 Azure 않습니다 하지 만들기, 업데이트 또는 hello 응용 프로그램에서 사용자 또는 그룹 개체를 제거 합니다. Hello 상태 백 tooon를 변경 하면 hello 서비스 toopick 중단 된 위치를 구성 합니다.

선택 hello **현재 상태를 지우고 동기화를 다시 시작** 확인란을 선택 하 고 중지 저장 hello 제공 서비스, 어떤 계정 Azure AD에 대 한 데이터를 캐시 하는 hello 덤프가 관리 hello 서비스를 다시 시작 하 고 hello 수행 초기 동기화를 다시 합니다. 이 옵션을 사용 하면 관리자 toostart hello를 다시 배포 프로세스를 프로 비전 합니다.

### <a name="synchronization-details"></a>동기화 세부 정보
이 섹션의 서비스를 프로 비전 하는 hello hello 작업에 대 한 추가 세부 정보를 제공, hello 첫 번째 및 마지막 시간 hello 제공 서비스를 포함 하 여 hello 응용 프로그램 및 사용자 및 그룹 개체의 수는 관리 되 고 실행 합니다.

Toohello 있도록 링크가 제공 됩니다 **프로 비전 작업 보고서**, 모든 사용자 및 그룹을 만든 Azure AD 간의 제거 및 업데이트에 대 한 로그를 제공 하는 hello 대상 응용 프로그램 및 toohello **오류 프로 비전 보고서** 더 자세한 오류 메시지에 대 한 사용자 및 그룹 읽기, 생성, 업데이트 또는 제거에 실패 한 toobe 해당 개체를 제공 합니다. 

##<a name="feedback"></a>사용자 의견

Azure AD 환경이 사용자의 마음에 들기를 바랍니다. 들어오는 hello 피드백을 유지 하세요! Hello에 피드백 및 개선 위한 아이디어 게시 **관리자 포털** 섹션 우리의 [피드백 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal)합니다.  에서는 매일 멋진 새로운 기능을 작성 하는 방법에 대 한 기대 하는 않는 및 사용 하 여 지침 tooshape 다음에 빌드 정의 합니다.


[0]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-blade.PNG
[1]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning.PNG
[2]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning-mapping.PNG
