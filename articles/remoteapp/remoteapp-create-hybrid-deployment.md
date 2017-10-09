---
title: "Azure RemoteApp 용 하이브리드 컬렉션 aaaHow toocreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate tooyour 내부 네트워크에 연결 하는 RemoteApp 배포 합니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>어떻게 toocreate Azure RemoteApp 용 하이브리드 컬렉션
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

다음과 같은 두 가지 종류의 Azure RemoteApp 컬렉션이 있습니다.

* 클라우드: Azure에 완전히 상주합니다. Hello 클라우드에서 toosave 모든 데이터를 선택할 수 있습니다 (되므로 클라우드 전용 컬렉션을) 또는 tooconnect 프로그램 컬렉션 tooa VNET 하 고 데이터를 저장 합니다.   
* 하이브리드: 가상 네트워크를 포함 하 hello 사용 하 여 Azure ad와 온-프레미스 Active Directory 환경 그러려면 온-프레미스 액세스-에 대 한 합니다.

필요한 사항을 모르십니까? [Azure RemoteApp에 필요한 컬렉션의 종류](remoteapp-collections.md)를 확인합니다.

이 자습서에서는 hello 하이브리드 컬렉션을 만드는 과정을 안내 합니다. 8가지 단계가 있습니다.

1. 작업을 결정 [이미지](remoteapp-imageoptions.md) toouse 컬렉션입니다. 사용자 지정 이미지를 만들거나 구독에 포함 된 hello Microsoft 이미지 중 하나를 사용할 수 있습니다.
2. 가상 네트워크를 설정합니다. 체크 아웃 hello [VNET 계획](remoteapp-planvnet.md) 및 [sizing](remoteapp-vnetsizing.md) 정보입니다.
3. 컬렉션을 만듭니다.
4. 컬렉션 tooyour 로컬 도메인에 가입 합니다.
5. 템플릿 이미지 tooyour 컬렉션을 추가 합니다.
6. 디렉터리 동기화를 구성합니다. Azure RemoteApp에는 어느 1) 구성 Azure Active Directory 동기화 hello 암호 동기화 옵션을 사용 하 여 Azure Active Directory 또는 2) 구성 Azure Active Directory 동기화 하지 않고 hello 암호 동기화 옵션은 도메인을 사용 하 여와 통합 필요 페더레이션된 tooAD FS 합니다. 체크 아웃 hello [RemoteApp과 함께 Active Directory에 대 한 구성 정보](remoteapp-ad.md)합니다.
7. RemoteApp 앱을 게시합니다.
8. 사용자 액세스를 구성합니다.

**시작하기 전에**

Hello 컬렉션을 만들기 전에 toodo hello 다음이 필요 합니다.

* [등록](https://azure.microsoft.com/services/remoteapp/) 합니다.
* Active Directory toouse에서 사용자 계정을 hello Azure RemoteApp 서비스 계정으로 만듭니다. 컴퓨터 toohello 도메인을만 연결할 수 있도록이 계정에 대 한 hello 권한을 제한 합니다.
* 온-프레미스 네트워크에 대한 정보 수집: IP 주소 정보 및 VPN 장치 세부 정보입니다.
* Hello 설치 [Azure PowerShell](/powershell/azure/overview) 모듈입니다.
* 에 액세스 하려면 toogrant hello 사용자에 대 한 정보를 수집 합니다. Azure Active Directory 사용자 계정 이름 hello 필요 합니다 (예를 들어 name@contoso.com) 각 사용자에 대 한 합니다. Azure AD 간에 UPN이 일치 하는 hello 있는지 확인 하 고 Active Directory 합니다.
* 템플릿 이미지를 선택합니다. Hello 앱 및 프로그램 사용자를 위해 toopublish 되도록 Azure RemoteApp 템플릿 이미지에 포함 되어 있습니다. 자세한 내용은 [Azure RemoteApp 이미지 옵션](remoteapp-imageoptions.md) 을 참조하세요.
* Toouse hello Office 365 ProPlus 이미지를 선택 하십시오. [여기](remoteapp-officesubscription.md)서 정보를 확인하세요.
* [RemoteApp에 대해 Azure Active Directory를 구성합니다](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>1단계: 가상 네트워크를 설정합니다.
기존 Azure 가상 네트워크를 사용하는 하이브리드 컬렉션을 배포하거나 새 가상 네트워크를 만들 수 있습니다. 가상 네트워크를 사용하여 사용자는 RemoteApp 원격 리소스를 통해 로컬 네트워크의 데이터에 액세스할 수 있습니다. Azure 가상 네트워크를 사용 하면 프로그램 컬렉션 네트워크에 직접 액세스 tooother Azure 서비스 및 가상 컴퓨터가 toothat 가상 네트워크를 배포 합니다.

Hello를 검토 해야 [VNET 계획](remoteapp-planvnet.md) 및 [VNET 크기](remoteapp-vnetsizing.md) 정보 VNET을 만들어야 합니다.

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>Azure VNET을 만들고 tooyour Active Directory 배포에 조인
[가상 네트워크](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)를 만들기 시작합니다. Hello에 이렇게 **네트워크** hello Azure 포털에서에서 탭 합니다. Tooconnect 사용자 가상 네트워크 toohello 동기화 된 tooyour Azure Active Directory 테 넌 트가 Active Directory 배포 해야 합니다.

참조 [hello Azure 포털을 사용 하 여 가상 네트워크 만들기](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) 자세한 정보에 대 한 합니다.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>가상 네트워크가 Azure RemoteApp에 대해 사용할 수 있는지 확인합니다.
컬렉션을 만들기 전에 새 가상 네트워크를 사용할 수 있는지 확인해 보겠습니다. Hello 다음을 수행 하 여이 확인할 수 있습니다.

1. RemoteApp에 대 한 방금 만든 hello 가상 네트워크의 서브넷을 hello 내 Azure 가상 컴퓨터를 만듭니다.
2. 원격 데스크톱 tooconnect toohello 가상 컴퓨터를 사용 합니다. ( **연결**을 클릭합니다.)
3. Toohello 가입 RemoteApp에 대 한 toouse 되도록 하는 동일한 Active Directory 배포 합니다.

작동했나요? 가상 네트워크 및 서브넷을 Azure RemoteApp에 사용할 수 있습니다!

Azure 가상 컴퓨터 만들기 및 원격 데스크톱을 사용 하 여 toothem를 연결 하는 방법에 대 한 자세한 정보를 찾을 수 [여기](https://msdn.microsoft.com/library/azure/jj156003.aspx)합니다.

## <a name="step-2-create-an-azure-remoteapp-collection"></a>2단계: Azure RemoteApp 컬렉션을 만듭니다.
1. Hello에 [Azure 포털](http://manage.windowsazure.com)이동, toohello Azure RemoteApp 페이지.
2. **새로 만들기 > VNET으로 만들기**를 클릭합니다.
3. 컬렉션의 이름을 입력합니다.
4. 표준 또는 기본 toouse-hello 계획을 선택 합니다.
5. Hello 드롭다운 목록 및 서브넷에서에서 VNET를 선택 합니다.
6. Toojoin 선택 것 tooyour 도메인입니다.
7. **RemoteApp 컬렉션 만들기**를 클릭합니다.

Azure RemoteApp 컬렉션을 만든 후 hello 컬렉션의 hello 이름을 두 번 클릭 합니다. 그러면 표시 hello **빠른 시작** 페이지-를 구성을 마친 hello 컬렉션입니다.

뭔가 잘못된 경우 체크 아웃 hello [문제 해결 정보는 하이브리드 컬렉션](remoteapp-hybridtrouble.md)합니다.

## <a name="step-3-link-your-collection-toohello-local-domain"></a>3 단계: 사용자 컬렉션 toohello 로컬 도메인 연결
1. Hello에 **빠른 시작** 페이지 **로컬 도메인에 가입**합니다.
2. Hello Azure RemoteApp 서비스 계정 tooyour 로컬 Active Directory 도메인을 추가 합니다. Hello 도메인 이름, 조직 구성 단위, 서비스 계정 사용자 이름 및 암호를 해야 합니다.
   
    이 hello에 나와 있는 단계를 준수 하는 경우 수집 된 hello 정보 [Azure RemoteApp에 대 한 Active Directory 구성](remoteapp-ad.md)합니다.

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>4 단계: 링크 tooan Azure RemoteApp 이미지
Azure RemoteApp 템플릿 이미지에는 사용자와 tooshare 되도록 하는 hello 프로그램이 포함 됩니다. 새 만들 수도 [템플릿 이미지](remoteapp-imageoptions.md) 또는 링크 tooan 기존 이미지 (하나를 이미 가져오거나 tooAzure RemoteApp 업로드) 합니다. Hello Azure RemoteApp의 tooone 연결할 수도 있습니다. [템플릿 이미지](remoteapp-images.md) Office 365 또는 Office 2013 (평가판 사용)에 대 한 프로그램을 포함 하는 합니다.

Tooenter hello 새 이미지를 업로드 하는 경우 해야 이름 hello 고 hello 이미지에 대 한 hello 위치를 선택 합니다. Hello hello 마법사의 다음 페이지를 복사 하는 PowerShell cmdlet-집합이 표시 하 고 관리자 권한 Windows PowerShell 프롬프트 tooupload hello 지정된 이미지에서 다음이 cmdlet을 실행 합니다.

Tooan 기존 템플릿 이미지를 연결 하는 경우 hello 이미지 이름, 위치 및 연결 된 Azure 구독을 지정 하면 됩니다.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>5단계 : Active Directory 디렉터리 동기화 구성
Azure RemoteApp에는 어느 1) 구성 Azure Active Directory 동기화 hello 암호 동기화 옵션을 사용 하 여 Azure Active Directory 또는 2) 구성 Azure Active Directory 동기화 하지 않고 hello 암호 동기화 옵션은 도메인을 사용 하 여와 통합 필요 페더레이션된 tooAD FS 합니다.

[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/)를 확인합니다. 이 문서는 4단계에서 디렉터리 통합을 설정하는 데 도움이 됩니다.

계획 정보 및 자세한 단계에 대해서는 [디렉터리 동기화 로드맵](http://msdn.microsoft.com//library/azure/hh967642.aspx) 을 참조하세요.

## <a name="step-6-publish-apps"></a>6단계: 앱 게시
Azure RemoteApp 앱 hello 앱 또는 프로그램 tooyour 사용자가 제공 하는 경우 업로드 한 hello 컬렉션에 대 한 hello 템플릿 이미지에 있습니다. 사용자가 응용 프로그램에 액세스 toorun 로컬 환경에 나타나지만 Azure에서 실행 중인 실제로 합니다.

Toopublish 해야 사용자가 앱에 액세스 하기 전에 이러한 – hello 원격 데스크톱 클라이언트를 통해 사용자가 액세스 hello 앱이 있습니다.

여러 앱 tooyour 컬렉션을 게시할 수 있습니다. Hello 게시 페이지에서 클릭 **게시** tooadd 응용 프로그램입니다. Hello에서 게시 하거나 **시작** 메뉴 hello 템플릿 이미지 또는 hello 앱에 대 한 hello 템플릿 이미지에 hello 경로 지정 하 여 합니다. Hello에서 tooadd를 선택 하면 **시작** 메뉴에서 프로그램 tooadd hello를 선택 합니다. Tooprovide hello 경로 toohello 앱을 선택 하면 hello 템플릿 이미지에 설치 되어 hello 경로 toowhere과 hello 앱에 대 한 이름을 제공 합니다.

## <a name="step-7-configure-user-access"></a>7단계: 사용자 액세스 구성
컬렉션을 만든 했으므로 tooadd hello 사용자가 원하는 toobe 수 toouse 원격 리소스 해야 합니다. hello Active Directory 테 넌 트에 대 한 액세스 tooneed tooexist hello 구독과 연관 제공 하는 hello 사용자 toocreate이 Azure RemoteApp 컬렉션을 사용 합니다.

1. Hello 빠른 시작 페이지에서 클릭 **사용자 액세스 구성**합니다.
2. 에 대 한 toogrant 액세스를 원하는 (Active Directory)에서 hello 회사 계정 또는 Microsoft 계정을 입력 합니다.
   
   **참고:**
   
   Hello를 사용 하면  *user@domain.com*  형식입니다.
   
   Office 365 ProPlus를 사용 하 여 컬렉션에는, 경우에 사용자에 대 한 hello Active Directory id를 사용 해야 합니다. 그러면 라이선스 유효성 검사에 도움이 됩니다.
3. Hello 사용자가 확인 되 면 클릭 **저장**합니다.

## <a name="next-steps"></a>다음 단계
Azure RemoteApp 하이브리드 컬렉션을 성공적으로 만들고 배포했습니다. hello 다음 단계는 toohave 사용자가 다운로드 하 여 hello 원격 데스크톱 클라이언트를 설치 합니다. 클라이언트 hello에 대 한 hello URL hello Azure RemoteApp 빠른 시작 페이지에서 찾을 수 있습니다. 클라이언트 hello에 사용자가 로그 이동한 hello 앱 게시에 액세스 합니다.

### <a name="help-us-help-you"></a>의견 보내기
또한 toorating에이 문서 및 설명 아래로 아래 변경할 수 있는 변경 내용을 toohello 문서 자체 알고 계십니까? 누락된 부분이 있나요? 잘못된 부분이 있나요? 혼동을 줄 수 있는 부분이 있나요? 위로 스크롤 및 클릭 **GitHub에서 편집** toomake 변경-것 나올지 검토를 위해 toous를 다음에 로그 오프 했습니다 되 면 확인할 수 있습니다 프로그램 변경 및 향상 바로 여기 합니다.

