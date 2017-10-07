---
title: "Azure RemoteApp의 클라우드 컬렉션 aaaHow toocreate | Microsoft Docs"
description: "데이터를 저장 하는 Azure RemoteApp의 배포 toocreate Azure 클라우드 hello 하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>어떻게 toocreate Azure RemoteApp의 클라우드 컬렉션
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

다음과 같은 두 가지 종류의 [Azure RemoteApp 컬렉션](remoteapp-collections.md)이 있습니다. 

* 클라우드: Azure에 완전히 상주합니다. Hello 클라우드에서 toosave 모든 데이터를 선택할 수 있습니다 (되므로 클라우드 전용 컬렉션을) 또는 tooconnect 프로그램 컬렉션 tooa VNET 하 고 데이터를 저장 합니다.   
* 하이브리드: 가상 네트워크를 포함 하 hello 사용 하 여 Azure ad와 온-프레미스 Active Directory 환경 그러려면 온-프레미스 액세스-에 대 한 합니다.

이 자습서에서는 hello 클라우드 컬렉션을 만드는 과정을 안내 합니다. 이 프로세스는 다음 4개의 단계로 구성됩니다. 

1. Azure RemoteApp 컬렉션을 만듭니다.
2. 선택적으로 디렉터리 동기화를 구성합니다. Azure AD를 사용 하는 경우 Active Directory에 있는 toosynchronize 사용자, 연락처 및 암호 온-프레미스 Active Directory tooyour Azure AD 테 넌 트에서 + 합니다.
3. 앱을 게시합니다.
4. 사용자 액세스를 구성합니다.

**시작하기 전에**

Hello 컬렉션을 만들기 전에 toodo hello 다음이 필요 합니다.

* [등록](https://azure.microsoft.com/services/remoteapp/) 합니다. 
* 에 액세스 하려면 toogrant hello 사용자에 대 한 정보를 수집 합니다. 이 정보는 사용자의 Microsoft 계정 정보나 Active Directory 작업 계정 정보가 될 수 있습니다.
* 이 절차에서는 가입의 일환으로 제공 하는 hello 템플릿 이미지의 하나 중 하나가 진행 중인 toouse 또는 이미 있는 toouse 사용할 hello 템플릿 이미지 업로드 가정 합니다. Tooupload 다른 템플릿 이미지에는 필요한 경우 hello 템플릿 이미지 페이지에서 시작할 수 있습니다. 클릭 하기만 **템플릿 이미지 업로드** hello 마법사의 hello 단계를 따릅니다. 
* Toouse hello Office 365 ProPlus 이미지를 선택 하십시오. [여기](remoteapp-officesubscription.md)서 정보를 확인하세요.
* Tooprovide 사용자 지정 앱 또는 LOB 프로그램을 선택 하십시오. 새 [이미지](remoteapp-imageoptions.md)를 만들어 클라우드 컬렉션에서 사용합니다.
* Tooconnect tooa VNET 해야 하는지 여부를 파악 합니다. Tooconnect tooa VNET을 선택 하면 hello에 맞는지 확인 [크기 조정 지침](remoteapp-vnetsizing.md) 맞는지 [tooRemoteApp 연결할 수](remoteapp-vnet.md)합니다. 체크 아웃 hello [VNET 계획 문서 ](remoteapp-planvnet.md)자세한 정보에 대 한 합니다.
* VNET을 사용 하는 경우 toojoin 만들지를 결정 하기 tooyour 로컬 Active Directory 도메인.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>1단계: VNET과 관계 없이 클라우드 컬렉션 만들기
사용 하 여 hello 다음 너무 단계**클라우드 전용 컬렉션을 만들**:

1. Hello 관리 포털에서 toohello RemoteApp 페이지로 이동 합니다.
2. **새로 만들기 > 빨리 만들기**를 클릭합니다.
3. 컬렉션의 이름을 입력하고 지역을 선택합니다.
4. 표준 또는 기본 toouse-hello 계획을 선택 합니다.
5. 이 컬렉션에 대 한 템플릿 toouse hello를 선택 합니다. 
   
    **팁:** RemoteApp에 대 한 구독와 함께 제공 [템플릿 이미지](remoteapp-images.md) Office 365를 포함 하는 또는 Office 2013 (평가판 사용)에 대 한 프로그램, 일부 (예: Word의 경우) 게시 등 toopublish 준비 합니다. 또한 새로운 [이미지](remoteapp-imageoptions.md) 를 만든 다음 클라우드 컬렉션에서 사용합니다.
6. **RemoteApp 컬렉션 만들기**를 클릭합니다.
   
    **중요:** 컬렉션 too30 분 tooprovision까지 걸릴 수 있으므로 합니다.

Azure RemoteApp 컬렉션을 만든 후 hello 컬렉션의 hello 이름을 두 번 클릭 합니다. 그러면 표시 hello **빠른 시작** 페이지-를 구성을 마친 hello 컬렉션입니다.

사용 하 여 hello 다음 toocreate 단계는 **클라우드 + VNET 컬렉션**:

1. Hello 관리 포털에서 toohello Azure RemoteApp 페이지로 이동 합니다.
2. **새로 만들기** > **VNET으로 만들기**를 클릭합니다.
3. 컬렉션의 이름을 입력합니다.
4. 표준 또는 기본 toouse-hello 계획을 선택 합니다.
5. 이미 만든 VNET hello를 선택 합니다. 모르는 어떻게 toodo 하 시겠습니까? 지금은 hello 단계는 hello [하이브리드](remoteapp-create-hybrid-deployment.md) 항목입니다.
6. 사용할지 toojoin 컬렉션 tooyour 도메인을 결정 합니다. 그렇다면 toouse AD Connect toointegrate Azure AD와 Active Directory 환경을 필요 합니다. 이 내용은 아래의 **2단계**에 나옵니다.
7. **RemoteApp 컬렉션 만들기**를 클릭합니다.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>2단계: Active Directory 디렉터리 동기화 구성(선택 사항)
Active Directory toouse 하려는 경우 Azure Active Directory 및 온-프레미스 Active Directory toosynchronize 사용자, 연락처 및 암호 tooyour Azure Active Directory 테 넌 트 간의 디렉터리 동기화 Azure RemoteApp에 필요 합니다. 계획에 대한 내용은 [Azure RemoteApp에 대해 Active Directory 구성](remoteapp-ad.md) 을 참조하세요. 수행할 수도 있습니다 직접 너무[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) 정보에 대 한 합니다.

## <a name="step-3-publish-apps"></a>3단계: 앱 게시
Azure RemoteApp 앱 hello 앱 또는 프로그램 tooyour 사용자가 제공 하는 경우 업로드 한 hello 컬렉션에 대 한 hello 템플릿 이미지에 있습니다. 응용 프로그램, hello 앱 사용자가 액세스 하는 경우 로컬 환경에서 toorun 나타나지만 Azure에서 가상 컴퓨터에서 실제로 실행. 

Toopublish 해야 사용자가 앱에 액세스 하기 전에 원격 데스크톱 클라이언트 hello에 – 앱 사용 하면 사용자가 액세스를 통해 hello 앱을 게시 합니다.

여러 앱 tooyour Azure RemoteApp 컬렉션을 게시할 수 있습니다. Hello 게시 페이지에서 클릭 **게시** tooadd 프로그램입니다. Hello에서 게시 하거나 **시작** 메뉴 hello 템플릿 이미지 또는 hello 앱에 대 한 hello 템플릿 이미지에 hello 경로 지정 하 여 합니다. Hello에서 tooadd를 선택 하면 **시작** 메뉴 hello 앱 toopublish를 선택 합니다. Tooprovide hello 경로 toohello 앱을 선택 하면 hello 템플릿 이미지에 설치 되어 hello 경로 toowhere과 hello 앱에 대 한 이름을 제공 합니다.

## <a name="step-4-configure-user-access"></a>4단계: 사용자 액세스 구성
컬렉션을 만든 했으므로 tooadd hello 사용자가 원하는 toobe 수 toouse 원격 리소스 해야 합니다. Active Directory를 사용 하는 hello Active Directory 테 넌 트에 대 한 액세스 tooneed tooexist hello 구독과 연관 제공 하는 hello 사용자가이 컬렉션 toocreate 사용.

1. Hello 빠른 시작 페이지에서 클릭 **사용자 액세스 구성**합니다. 
2. 에 대 한 toogrant 액세스를 원하는 (Active Directory)에서 hello 회사 계정 또는 Microsoft 계정을 입력 합니다.
   
   **참고:** 
   
   Hello를 사용 하면  *user@domain.com*  형식입니다.
   
   Office 365 ProPlus를 사용 하 여 컬렉션에는, 경우에 사용자에 대 한 hello Active Directory id를 사용 해야 합니다. 그러면 라이선스 유효성 검사에 도움이 됩니다. 
3. Hello 사용자가 확인 되 면 클릭 **저장**합니다.

## <a name="next-steps"></a>다음 단계
Azure RemoteApp 클라우드 컬렉션을 만들고 배포했습니다. hello 다음 단계는 toohave 사용자가 다운로드 하 여 hello 원격 데스크톱 클라이언트를 설치 합니다. 클라이언트 hello에 대 한 hello URL hello Azure RemoteApp 빠른 시작 페이지에서 찾을 수 있습니다. 클라이언트 hello에 사용자가 로그 이동한 hello 앱 게시에 액세스 합니다.

### <a name="help-us-help-you"></a>의견 보내기
또한 toorating에이 문서 및 설명 아래로 아래 변경할 수 있는 변경 내용을 toohello 문서 자체 알고 계십니까? 누락된 부분이 있나요? 잘못된 부분이 있나요? 혼동을 줄 수 있는 부분이 있나요? 위로 스크롤 및 클릭 **GitHub에서 편집** toomake 변경-것 나올지 검토를 위해 toous를 다음에 로그 오프 했습니다 되 면 확인할 수 있습니다 프로그램 변경 및 향상 바로 여기 합니다.

