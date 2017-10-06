---
title: "aaaHow toouse Azure RemoteApp과 함께 Office 365 구독 | Microsoft Docs"
description: "Azure RemoteApp tooshare Office 앱에 Office 365 구독을 사용 하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: f82b6e23-2b71-47be-846d-fd93f2652f3c
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2648868dd28cbcd93e38461ae6dce25eaa5d5e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-your-office-365-subscription-with-azure-remoteapp"></a>어떻게 toouse Azure RemoteApp과 함께 Office 365 구독
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Hello 클라우드에서 Azure RemoteApp tooshare 오피스 응용 프로그램에 기존 Office 365 구독을 사용할 수 있는 것을 아십니까? Office 365 + Azure RemoteApp 옵션에 대 한 내용은에서 읽을 수 있는 Office 365에 대 한 포함 하 여 링크 tooarticles 확인 가장 hello 가입 합니다.

## <a name="how-do-i-use-office-365-accounts-for-azure-remoteapp"></a>Azure RemoteApp에 Office 365 계정을 사용하는 방법
모든 정보를 hello에 대 한 새 아티클을 Peter의 확인해: [어떻게 Office 365 사용자 계정으로 Azure RemoteApp toouse](remoteapp-o365user.md)

## <a name="can-i-use-my-office-365-subscription-toorun-office-applications-in-azure-remoteapp"></a>Azure RemoteApp에서 내 Office 365 구독 toorun Office 응용 프로그램을 사용할 수 있습니까?
예! 사실, Office 365 구독을 사용 하는 hello 방법은 toobring만 Office 응용 프로그램 tooAzure RemoteApp 합니다.

(참고: Azure RemoteApp 배포 호스팅 파트너에서 배달 하는 경우에 따라 Office 라이선스로 있습니다 수 tooprovide 될 수 있습니다는 [서비스 공급자 사용권 계약](http://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx))

hello Office 365 구독에 대 한 큰 장점 중 하나는 여러 다른 플랫폼과 hello Azure 클라우드를 비롯 한 환경에서 동일한 사용자 라이선스를 hello 사용할 수 있습니다. Azure RemoteApp의 Office 응용 프로그램을 사용 하면 toopurchase 추가 라이선스 필요 하지 않거나 기존 라이선스 특별 하 게에서 구성 해야 합니다. [Office 365 ProPlus](https://technet.microsoft.com/library/Gg702619.aspx)를 포함하는 Office 365 구독만 필요합니다.

Office 365 ProPlus를 사용하면 [공유 컴퓨터 인증](https://technet.microsoft.com/library/Dn782860.aspx)이 가능합니다. 이 기능을 사용하면 Azure RemoteApp(및 원격 데스크톱 서비스)과 같은 가상 및 클라우드 환경에서 Office에 대한 임시 사용자 기반을 활성화할 수 있습니다.

어떤 Office 365 계획이 Office 365 ProPlus를 포함하나요? 체크 아웃 hello [각 계획 내에서 가용성을 서비스](https://technet.microsoft.com/library/office-365-plan-options.aspx) 테이블입니다. 모든 계획 포함 Office 365 ProPlus (예를 들어 hello Office 365 비즈니스 계획) note 합니다. 계획에 표시 되지 않는 경우 (예: Office 365 Education E3)을 수행 하는 tooa 계획을 업그레이드 하는 것이 좋습니다.

## <a name="ok-so-how-are-my-office-365-proplus-licenses-used-with-azure-remoteapp"></a>이제 그래서 Azure RemoteApp와 함께 사용하는 Office 365 ProPlus 라이선스는 어떻나요?
Office 365 ProPlus에 대 한 각 사용자 라이선스를 too5 컴퓨터와 태블릿 및 휴대폰에 Office 응용 프로그램을 활성화할 사용자를 한 명이 수 있습니다. Office hello 장치에서 비활성화 될 때까지 각 활성화 hello 사용자로 등록 됩니다. (사용자 hello에 자신의 장치를 관리할 수 있습니다 [Office 365 포털](https://portal.office365.com/).)

Azure RemoteApp과 함께 단일 사용자를 기록할 수 있습니다 hello에 여러 컴퓨터에 동일한 것을 모르고 일 합니다. Hello 서비스에서 자동으로 관리 하 고 hello 앱 및 프로그램 공유한 hello 사용자에 게 표시 하는 동안 hello 클라우드에서 리소스 크기를 조정 때문입니다. 즉, 해당 사용자 toodo 필요 하지 않은-Office 365 ProPlus이 시나리오는 공유 컴퓨터 정품 인증 모드를 제공에 대 한 모든 라이선스 관리 tooaccess 이러한 리소스 및 해당 hello 개별 컴퓨터에 포함 되지 않습니다 hello 5 컴퓨터 정품 인증 제한 합니다.

Tooyour 사용자가 Office 365 ProPlus 라이선스를 할당 하면 (admin 님 안녕하세요)으로 자신의 개인 장치 뿐 아니라 Azure RemoteApp 컬렉션을 통해 Office를 사용할 수 있습니다.

## <a name="which-office-applications-can-i-use-with-office-365-and-azure-remoteapp"></a>어떤 Office 응용 프로그램을 Office 365 및 Azure RemoteApp과 함께 사용할 수 있나요?
Office 365 구독 tooactivate 사용 및 Azure RemoteApp 배포에서는 Office 2013을 공유할 수 있습니다. 현재 다른 버전의 Azure RemoteApp과 함께 Office hello 사용을 지원 하지 않습니다. 여기에는 Office 2003, Office 2007, Office 2010 및 Office 2016이 포함됩니다.

## <a name="what-about-visio-pro-or-project-pro"></a>Visio Pro 또는 Project Pro의 경우는 어떤가요?
RemoteApp 구독에 포함 된 hello Office 365 ProPlus 이미지에는 Visio Pro 및 프로젝트 Pro 모두 포함 됩니다. 하지만 Office 365 ProPlus 구독 tooactivate 사용자는 프로그램에 사용할 수 없습니다-파일은 각각 고유한 라이선스가 합니다. Hello에 활성화할 수 [Office 365 포털](https://portal.office365.com/)합니다. 

없는 toolicense 이러한 프로그램 toouse 하지 않으려면 해당 합니다. 바로 활성화 hello 프로그램 toouse-을 건너뛰고 다른 hello 합니다. Hello 이미지에 계속 표시 됩니다 있지만 사용할 수 없습니다. 

## <a name="how-do-i-get-started-with-office-365-and-azure-remoteapp"></a>어떻게 Office 365 및 Azure RemoteApp을 시작하나요?
Office 365 라이선스의 hello 세부 정보를 파악 했으므로 액세스할 Azure RemoteApp에서 사용 하 여 시작할 수 있습니다-매우 쉽습니다.

Azure RemoteApp 컬렉션을 만들 때 사용 하 여 hello **Office 365 ProPlus (구독 필요)** 이미지입니다.

![Office 365 Pro Plus와 Azure RemoteApp 이미지](./media/remoteapp-officesubscription/remoteapp-officeimage.png)

이 이미지는 hello 최신 버전의 Windows Server 및 Office 365 ProPlus를 포함합니다. 컬렉션(게시 앱 포함)을 구성한 후에 (RemoteApp 클라이언트를 사용하여) Azure RemoteApp에 로그인하고 Office 앱에 Office 365 자격 증명을 제공합니다. 라이선스는 필요한 설정 또는 관리 없이 자동으로 제공됩니다.

## <a name="can-i-create-a-custom-image-with-office-365-proplus"></a>Office 365 ProPlus를 사용하여 사용자 지정 이미지를 만들 수 있나요?
Office 365 ProPlus를 포함하는 컬렉션에 사용자 지정 이미지를 만들 수 있습니다. 두 가지 방법이-제공 hello Azure 갤러리 이미지를 사용 하거나 사용자 지정 이미지 만들고 수 있는 Office 365 ProPlus를 설치 합니다.

### <a name="use-hello-azure-gallery-image"></a>Hello Azure 갤러리 이미지를 사용 하 여
hello 가장 쉬운 방법은 toodeploy Office 365 ProPlus tooa 컬렉션은 너무[hello Azure 갤러리 이미지 중 하나로 시작](remoteapp-image-on-azurevm.md) Azure RemoteApp 구독에 포함 되어 있습니다. Hello를 선택 해야 **Windows Server 원격 데스크톱 세션 호스트와 Office 365 ProPlus 미리 설치 되어** 이미지입니다. 그런 다음 해당 이미지에 원하는 다른 모든 앱을 설치 하 고 계속 진행 하세요 toogo 합니다.

### <a name="use-a-custom-image"></a>사용자 지정 이미지 사용
항상 사용자 지정 이미지를 만들 수 있습니다-만들 수는 [Azure VM](remoteapp-image-on-azurevm.md) 또는 [hello 이미지 로컬로 만들기](remoteapp-create-custom-image.md) tooAzure 업로드 합니다. 두 경우 모두 Office 365 ProPlus hello 공유 컴퓨터 활성화 노드를 사용 하 여 설치 해야 합니다. 사용 하 여 hello [Office 배포 도구](http://blogs.technet.com/b/odsupport/archive/2014/07/11/using-the-office-deployment-tool.aspx) hello에 따라 [지침](https://technet.microsoft.com/library/Dn782858.aspx) 설치에 대 한 합니다.  

### <a name="disable-automatic-updates-for-office-365-proplus-in-your-custom-image---important"></a>사용자 지정 이미지에서 Office 365 ProPlus에 대한 자동 업데이트를 사용하지 않도록 설정합니다. 중요합니다.
사용자 지정 이미지는 사용자가 향상 hello 요청을 추가 리소스를 추가 하기 위한 템플릿으로 Azure RemoteApp에서 사용 됩니다. tooprevent 지연 및 연결 문제는 hello 이미지에 Office를 자동 업데이트를 비활성화 합니다. 이렇게 하지 않으면 시작할 때 해당 템플릿으로 만든 모든 리소스가 자동으로 업데이트됩니다. 대신, 사용자 지정 이미지를 업데이트 하기 위한 hello 표준 Azure RemoteApp 프로세스를 사용 합니다. 이런 방식으로 hello 템플릿 이미지에 한 번 hello Office 응용 프로그램을 업데이트 한 다음 tooyour 사용자 hello 업데이트를 받고 처리 하는 Azure RemoteApp을 사용 합니다.

toodisable 자동 업데이트를 hello 다음 toohello Office 배포 도구 구성 파일을 추가 합니다.

        <Updates Enabled="FALSE" />

그래서 구성 파일에 다음 줄이 포함되어야 합니다.

        <Display Level="NONE" AcceptEULA="TRUE" />
        <Property Name="SharedComputerLicensing" Value="1" />
        <Updates Enabled="FALSE" />

## <a name="so-how-can-i-update-an-image-with-office-365-proplus"></a>그래서 어떻게 Office 365 ProPlus로 이미지를 업데이트할 수 있나요?
컬렉션에 여러 이유로 tooupdate hello 이미지가 있습니다. 다음에 몇몇 이유가 있습니다.

* Hello 최신 Windows 업데이트 가져오기 
* Hello 최신 Office 365 ProPlus 응용 프로그램 업데이트
* 사용자 지정 앱 업데이트
* Hello 이미지 자체에 대 한 기타 구성 설정 변경

업데이트 했으며 컬렉션 toouse hello 이미지를 업데이트 하기 위한 종단 간 단계 hello에 대 한 이동 [여기](remoteapp-update.md)합니다. 하지만 이미지와 Office 365 ProPlus tooupdate hello 하는 방법에 대 한 내용은 다음 정보는 hello 확인 합니다.

이미지를 업데이트하는 데 두 가지 옵션이 있습니다. 이미지를 완전히 새로운 것으로 대체하거나 수동으로 기존 이미지를 업데이트합니다.

### <a name="replace-your-image-with-hello-latest-azure-gallery-image--add-customizations"></a>Hello 최신 Azure 갤러리 이미지와 이미지를 바꿉니다 + 사용자 지정 내용을 추가합니다
이 옵션을 사용 하면 고객이 Microsoft가 hello Windows 서버 및 Office 365 ProPlus 업데이트 관리 합니다. 기존 이미지를 업데이트 하는 대신 hello 최신 갤러리 이미지를 기반으로 완전히 새로운 이미지를 만듭니다. 그런 다음 toocustomize hello 이미지-이전과 동일한 단계를 수행할 사용자 지정 앱을 설치, 수정 등 hello 이미지 구성을 반복 합니다.

hello 갤러리 이미지는 쉽게 재설정할 수 있습니다, Windows Server 및 Office 365 ProPlus 앱 toodate 중인지를 알고 있으면 되므로 정기적으로 업데이트 됩니다. 물론, hello 대신 수 있는 경우 tooapply 사용자 지정 내용이 새 이미지를 받을 때마다 됩니다. 사용자 지정 설정 스크립트 tooautomate를 만들 수 있습니다.

### <a name="manually-update-your-existing-image"></a>기존 이미지를 수동으로 업데이트
이 옵션을 표준 Windows 도구 tooapply 업데이트 toohello 이미지를 사용합니다. Office 365 ProPlus에 대 한 Office 배포 도구 toodownload hello를 사용 하 고 hello 최신 업데이트 또는 버전의 Office 365 ProPlus를 설치 합니다.

> [!IMPORTANT]
> 기억-hello Office 365 ProPlus 자동 업데이트를 사용 하지 않도록 설정 합니다.
> 
> 

업데이트를 위한 hello Office 배포 도구를 사용 하는 방법에 대 한 자세한 정보가 필요한 경우

* [간편 실행을 hello Office 배포 도구를 사용 하 여 Office 365 제품에 대 한 배포](https://technet.microsoft.com/library/JJ219423.aspx)
* [배포 및 업데이트 Office 365 ProPlus를 사용 하 여 hello Office 배포 도구](https://channel9.msdn.com/Events/Ignite/2015/BRK3168) (비디오)
* [Office 365 ProPlus에 대한 업데이트 설정 구성](https://technet.microsoft.com/library/dn761708.aspx)

