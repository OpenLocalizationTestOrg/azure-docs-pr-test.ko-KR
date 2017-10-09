---
title: "aaaWhat은 Azure RemoteApp 이란? | Microsoft Docs"
description: "자세한 내용은 방법 Azure RemoteApp을 통해 tooshare 앱 및 리소스 tooany 장치입니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>Azure RemoteApp이란?
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp은 원격 데스크톱 서비스 tooAzure 뒷받침 되며 hello 온-프레미스 Microsoft RemoteApp 프로그램의 hello 기능을 제공 합니다. Azure RemoteApp을 사용 하면 다양 한 사용자 장치에서 안전 하 게 원격 액세스 tooapplications 제공할 수 있습니다. 기본적으로 azure RemoteApp hello 클라우드에서 비 영구적인 터미널 서버 세션을 호스트 그리고 toouse를 가져와서 해당 사용자와 공유 합니다.

Azure RemoteApp를 사용하면 거의 모든 장치의 사용자와도 앱 및 리소스를 공유할 수 있습니다. Hello 하드웨어의 의미 및 toomeet 사용자 요구를 크기 조정 hello 클라우드에서 앱을 호스트 하는 것 Toodo 됩니다 tooshare, 한 다음 사용자가 toouse 해당 앱을 얻는 hello 앱을 업로드 합니다. [사용자가 자신의 장치를 tookeep 얻는](remoteapp-clients.md)hello Azure 포털을 통해 모든 항목을 관리 하는 반면, 합니다. 도 앱 및 데이터 hello 보안을 유지할 수 있으므로 회사 자격 증명을 사용 하 여 hello 옵션이 제공 됩니다.

Azure RemoteApp에 대한 자세한 내용을 읽거나 이미 확신을 가진 경우 [지금 사용해 보세요](https://azure.microsoft.com/services/remoteapp/).

Azure RemoteApp과 관련된 질문이 있는 경우 [FAQ](remoteapp-faq.md)를 확인하세요.

Azure RemoteApp hello의 일부인 [Microsoft 가상 데스크톱 인프라](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx)합니다.

**신규!** Azure RemoteApp에 대 한 자세한 toolearn를 선택 하십시오. 또는 규모에 Azure RemoteApp toovalidate 준비 됨? 우리의 매주 가입 [hello 전문가 게 문의 웹 세미나](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website)합니다.

## <a name="azure-remoteapp-collections"></a>Azure RemoteApp 컬렉션
다음과 같은 두 가지 종류의 [Azure RemoteApp 컬렉션](remoteapp-collections.md)이 있습니다.

* A **컬렉션 클라우드** 에서 호스트 되 고 hello 클라우드에서 프로그램에 대 한 데이터를 저장 합니다. 사용자는 Microsoft 계정이나 Azure Active Directory와 동기화 또는 페더레이션된 회사 자격 증명으로 로그인하여 앱에 액세스할 수 있습니다.
  
    클라우드 컬렉션 선택 tooshare 원하는 hello 응용 프로그램 연결 tooany 리소스가 필요 하지 않는 경우 회사의 개인 네트워크 (예: 전자 VPN 장치). 있는 경우 hello 응용 프로그램 리소스를 사용 하 여 hello 인터넷, OneDrive 또는 Azure에서 클라우드 컬렉션은 적합 합니다. Hello 가장 빠른 toocreate 이기도합니다.
* A **하이브리드 컬렉션** 에서 호스팅되며 hello Azure 클라우드 있지만 데이터에 액세스 하면 사용자와 로컬 네트워크에 저장 된 리소스에 데이터를 저장 합니다. 사용자는 Azure Active Directory와 동기화 또는 페더레이션된 회사 자격 증명으로 로그인하여 앱에 액세스할 수 있습니다.
  
    회사의 개인 네트워크에 연결 tooresources 필요한 경우 하이브리드 컬렉션을 선택 합니다. 예를 들어 경우 hello 응용 프로그램 tooone hello 다음의 액세스 필요:
  
  * 인트라넷에 위치한 파일 서버
  * Quicken
  * 방화벽 뒤에 있는 데이터베이스
    
    이것은 대기업 이라도 수 없는 개인 네트워크에서 많은 리소스 이동 toohello 클라우드 더 유용 합니다.

hello 다양 한 컬렉션 네트워크를 포함 하 여 다양 한 옵션, 따라서 파악 [어떤 컬렉션](remoteapp-collections.md) 가장 적합 합니다. 

### <a name="updating-your-collection"></a>컬렉션 업데이트
Hello hello 클라우드 및 하이브리드 컬렉션 간의 주요 차이점 중 하나는 소프트웨어 업데이트 처리 방법입니다. Hello 사전 설치 된 Office 365 ProPlus 또는 Office 2013 이미지를 사용 하는 클라우드 컬렉션에 없는 모든 업데이트에 대 한 tooworry 합니다. hello 서비스 자체를 유지 관리 하 고 지속적으로, tooboth 앱 및 hello 운영 체제에서는 업데이트 합니다.

하이브리드 컬렉션의 경우와 같은 사용자 지정 템플릿 이미지를 사용 하는 클라우드 컬렉션을 담당 하는 hello 이미지 및 응용 프로그램 유지 관리 합니다. 도메인에 가입된 이미지의 경우 Windows 업데이트, 그룹 정책 또는 System Center와 같은 도구를 사용하여 업데이트를 제어할 수 있습니다.

사용자 지정 템플릿 이미지를 업데이트 한 후에 hello 새 이미지 toohello Azure 클라우드 업로드 한 다음 hello 컬렉션 toouse hello 새 이미지를 업데이트 합니다. (Hello Azure RemoteApp에서에서 이렇게 하려면 **빠른 시작** 페이지 또는 대시보드를 환영 합니다.)

자세한 내용은 [컬렉션 업데이트](remoteapp-update.md) 를 참조하세요.

## <a name="supported-remoteapp-clients"></a>지원되는 RemoteApp 클라이언트
Azure RemoteApp Mac, iOS 및 Android 용 hello Microsoft 원격 데스크톱 앱 뿐만 아니라 Windows 및 Windows RT에 대 한 hello RemoteApp 클라이언트 앱에서 지원 됩니다. 사용자가 자신의 모바일에서 이러한 앱을 사용 하거나 장치 tooaccess hello 새 Azure RemoteApp 프로그램 계산 수 있습니다.

참조 [Azure RemoteApp에 앱 액세스](remoteapp-clients.md) hello 클라이언트에 대 한 자세한 내용은 합니다.

## <a name="next-steps"></a>다음 단계
지금 사용해 보세요! 다음은 Azure RemoteApp를 시작하는 데 도움이 되는 문서입니다.

* [Azure RemoteApp에 필요한 컬렉션의 종류는 무엇입니까?](remoteapp-collections.md)
* [Azure RemoteApp 이미지 만들기](remoteapp-imageoptions.md)
* [어떻게 toocreate Azure RemoteApp의 클라우드 컬렉션](remoteapp-create-cloud-deployment.md)
* [어떻게 toocreate Azure RemoteApp의 하이브리드 컬렉션](remoteapp-create-hybrid-deployment.md)
* [Azure RemoteApp의 라이선스 작동 방식](remoteapp-licensing.md)
* [Azure RemoteApp 사용 모범 사례](remoteapp-bestpractices.md)
* [Azure RemoteApp FAQ](remoteapp-faq.md)

### <a name="help-us-help-you"></a>의견 보내기
또한 toorating에이 문서 및 설명 아래로 아래 변경할 수 있는 변경 내용을 toohello 문서 자체 알고 계십니까? 누락된 부분이 있나요? 잘못된 부분이 있나요? 혼동을 줄 수 있는 부분이 있나요? 위로 스크롤 및 클릭 **GitHub에서 편집** 또는 **편집** toomake 변경-것 나올지 검토를 위해 toous를 다음에 로그 오프 했습니다 되 면 확인할 수 있습니다 프로그램 변경 및 향상 바로 여기 합니다.

