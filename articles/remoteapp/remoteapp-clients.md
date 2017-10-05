---
title: "모든 장치에서 앱에 액세스 | Microsoft Docs"
description: "Azure RemoteApp에 지원되는 클라이언트 및 앱에 액세스하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 10a5be6251765b59fac92a33120cedcf8091a677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a>Azure RemoteApp에서 앱에 액세스
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.
> 
> 

Azure RemoteApp의 장점 중 하나는 앱을 모든 장치에서 액세스할 수 있다는 것입니다. 한 장치에서 작업을 시작한 다음 두 번째 장치로 매끄럽게 전환하고 중지한 위치에서 바로 시작할 수도 있습니다. 시작하려면 장치에 적절한 클라이언트를 다운로드하고 서비스에 로그인해야 합니다.

이 항목에서는 각 클라이언트에서 RemoteApp에 로그인하는 방법에 앞서 현재 지원되는 클라이언트 및 다운로드 방법을 살펴보겠습니다.

## <a name="supported-clients"></a>지원되는 클라이언트
장치가 다음 운영 체제 중 하나를 실행하는 경우 아래 단계에 따라 RemoteApp에 액세스할 수 있습니다.

* Windows 10 
* Windows 8.1
* Windows 8
* Windows 7 서비스 팩 1
* Windows Phone 8.1
* iOS
* Mac OS X
* Android

 씬 클라이언트의 경우 다음과 같은 Windows Embedded 씬 클라이언트가 지원됩니다.

* Windows Embedded Standard 7
* Windows Embedded 8 Standard
* Windows Embedded 8.1 Industry Pro
* Windows 10 IoT Enterprise

## <a name="downloading-the-client"></a>클라이언트 다운로드
사용하는 플랫폼에 관계없이 [원격 데스크톱 클라이언트 다운로드](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) 페이지에서 RemoteApp에 액세스하는 데 필요한 클라이언트를 찾을 수 있습니다.

다양한 링크를 클릭하여 바로 클라이언트 다운로드를 시작하거나 해당 플랫폼에 대한 앱 스토어의 클라이언트 다운로드 페이지로 이동합니다. 화면의 지침에 따라 클라이언트를 설치합니다.

장치에 클라이언트를 설치하고 시작한 후 아래의 해당 섹션으로 이동하여 클라이언트에서 RemoteApp에 로그인하는 방법을 알아봅니다.

## <a name="android"></a>Android
Google Play 스토어에서 Microsoft 원격 데스크톱 앱을 설치하고 나면 앱 목록의 **원격 데스크톱**아래에서 찾을 수 있습니다.

1. 아직 앱을 사용한 적이 없는 경우 앱을 시작하면 빈 연결 센터로 이동됩니다. Azure RemoteApp을 시작하려면 **"" +""** 추가 단추, **Azure RemoteApp**을 차례로 탭합니다.    
   
     ![빈 연결 센터](./media/remoteapp-clients/Android1.png)
2. 서비스에 액세스하려면 메일 주소로 로그인해야 합니다. **시작**을 탭합니다.
   
    ![로그인 프롬프트](./media/remoteapp-clients/Android2.png)
3. 다음 페이지에서 **메일 주소**를 입력하고 **계속**을 탭합니다. Azure Active Directory를 사용하여 로그인 프로세스가 시작됩니다.
   
    ![첫 번째 Azure Active Directory 페이지](./media/remoteapp-clients/Android3.png)
4. 화면의 지침에 따라 Microsoft 계정(이전 "LiveID") 또는 조직 ID로 로그인합니다. 로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다. 표시되는 경우 신뢰하는 초대를 선택하고 **완료**를 탭합니다.    
   
    ![초대 페이지](./media/remoteapp-clients/Android4.png)
5. 초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다. 앱 중 하나를 탭하여 시작하고 사용합니다.
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/Android5.png)
6. 아직 초대가 없는 경우에도 서비스를 체험할 수 있습니다. 이렇게 하려면 메시지가 표시될 때 **무료 평가판으로 이동** 을 탭합니다.
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/Android6.png)
7. 이 경우 RemoteApp을 시작하기 위한 기본적인 앱 집합에 액세스할 수 있습니다.
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a>iOS
앱 스토어에서 Microsoft 원격 데스크톱 앱을 설치하고 나면 앱 목록의 **RD 클라이언트**아래에서 찾을 수 있습니다.

1. 아직 앱을 사용한 적이 없는 경우 앱을 시작하면 빈 연결 센터로 이동됩니다. Azure RemoteApp을 시작하려면 **"" +""** 추가 단추, **Azure RemoteApp 추가**를 차례로 탭합니다.
   
    ![빈 연결 센터](./media/remoteapp-clients/IOS1.png)
2. 서비스에 액세스하려면 메일 주소로 로그인해야 합니다. 해당 프로세스를 시작하려면 **메일 주소**를 입력하고 **계속**을 탭합니다.
   
    ![로그인 프롬프트](./media/remoteapp-clients/picture1.png)
3. 화면의 지침에 따라 Microsoft 계정(LiveID) 또는 조직 ID로 로그인합니다. 로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다. 표시되는 경우 신뢰하는 초대를 선택하고 **완료**를 탭합니다.
   
    ![초대 페이지](./media/remoteapp-clients/IOS3.png)
4. 초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다. 앱 중 하나를 탭하여 시작하고 사용합니다.
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/IOS4.png)
5. 아직 초대가 없는 경우에도 서비스를 체험할 수 있습니다. 이렇게 하려면 메시지가 표시될 때 **무료 평가판으로 이동** 을 탭합니다.
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/IOS5.png)
6. 이 경우 RemoteApp을 시작하기 위한 기본적인 앱 집합에 액세스할 수 있습니다.
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a>Mac OS X
앱 스토어에서 Microsoft 원격 데스크톱 앱을 설치하고 나면 앱 목록의 **Microsoft 원격 데스크톱**아래에서 찾을 수 있습니다.

1. 아직 앱을 사용한 적이 없는 경우 앱을 시작하면 빈 연결 센터로 이동됩니다. Azure RemoteApp을 시작하려면 **Azure RemoteApp** 단추를 클릭합니다.
   
    ![빈 연결 센터](./media/remoteapp-clients/Mac1.png)
2. 서비스에 액세스하려면 메일 주소로 로그인해야 하며, 해당 프로세스를 시작하려면 **시작**을 탭합니다.
   
    ![로그인 프롬프트](./media/remoteapp-clients/Mac2.png)
3. 다음 페이지에서 **메일 주소**를 입력하고 **계속**을 탭합니다. Azure Active Directory를 사용하여 로그인 프로세스가 시작됩니다.
   
    ![첫 번째 Azure Active Directory 페이지](./media/remoteapp-clients/picture2.png)
4. 화면의 지침에 따라 Microsoft 계정(LiveID) 또는 조직 ID로 로그인합니다. 로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다. 표시되는 경우 신뢰하는 초대를 선택하고 대화 상자를 닫습니다.
   
    ![초대 페이지](./media/remoteapp-clients/Mac4.png)
5. 초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다. 앱 중 하나를 두 번 클릭하여 시작하고 사용합니다.
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/Mac5.png)
6. 아직 초대가 없는 경우에도 서비스를 체험할 수 있습니다. 이렇게 하려면 메시지가 표시될 때 **무료 평가판으로 이동** 을 클릭합니다.
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/Mac6.png)
7. 이 경우 RemoteApp을 시작하기 위한 기본적인 앱 집합에 액세스할 수 있습니다.
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a>Windows(Windows Phone을 제외하고 지원되는 모든 버전)
설치가 완료되면 클라이언트가 자동으로 시작되지만 나중에 다시 액세스해야 하는 경우 앱 목록의 **Azure RemoteApp**아래에서 찾을 수 있습니다.

1. 클라이언트를 시작한 후 표시되는 첫 페이지는 Azure RemoteApp 시작 페이지입니다. 계속하려면 **시작**을 클릭합니다.
   
    ![Azure RemoteApp 클라이언트의 시작 페이지](./media/remoteapp-clients/Windows1.png)
2. 다음 페이지는 Azure Active Directory를 사용하여 Azure RemoteApp에 대한 로그인 프로세스를 시작합니다. 이전에 Microsoft 서비스를 사용한 적이 있다면 이 프로세스가 익숙할 것입니다. **메일 주소**를 입력하고 **계속**을 클릭합니다.
   
    ![첫 번째 Azure Active Directory 프롬프트](./media/remoteapp-clients/Windows2.png)
3. 화면의 지침에 따라 Microsoft 계정(LiveID) 또는 조직 ID로 로그인합니다. 로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다. 표시되는 경우 신뢰하는 초대를 선택하고 **완료**를 클릭합니다.
   
    ![Azure RemoteApp 클라이언트의 초대 페이지](./media/remoteapp-clients/Windows3.png)
4. 초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다. 앱 중 하나를 두 번 클릭하여 시작하고 사용합니다.
   
    ![Azure RemoteApp 클라이언트의 연결 센터](./media/remoteapp-clients/Windows4.png)
5. 아직 초대를 받지 못한 경우에도 걱정할 필요가 없습니다. 데모 컬렉션에 액세스하여 서비스를 테스트할 수 있습니다.
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a>Windows Phone 8.1
Windows Phone 8.1 스토어에서 Microsoft 원격 데스크톱 앱을 설치하고 나면 앱 목록의 **원격 데스크톱**아래에서 찾을 수 있습니다.

1. 아직 앱을 사용한 적이 없는 경우 앱을 시작하면 빈 연결 센터로 바로 이동됩니다. Azure RemoteApp을 시작하려면 화면 맨 아래의 추가 단추 **""+""** 를 탭합니다.
   
    ![빈 연결 센터](./media/remoteapp-clients/WinPhone1.png)
2. **Azure RemoteApp**을 탭합니다.
   
    ![항목 추가 페이지](./media/remoteapp-clients/WinPhone2.png)
3. 서비스에 액세스하려면 메일 주소로 로그인해야 하며, 해당 프로세스를 시작하려면 **연결**을 탭합니다.
   
    ![로그인 프롬프트](./media/remoteapp-clients/WinPhone3.png)
4. 다음 페이지에서 **메일 주소**를 입력하고 **계속**을 탭합니다. Azure Active Directory를 사용하여 로그인 프로세스가 시작됩니다.
   
    ![첫 번째 Azure Active Directory 페이지](./media/remoteapp-clients/WinPhone4.png)
5. 화면의 지침에 따라 Microsoft 계정(LiveID) 또는 조직 ID로 로그인합니다. 로그인된 후 수신한 모든 초대를 나열하는 페이지가 표시될 수도 있습니다. 표시되는 경우 신뢰하는 초대를 선택하고 **저장**을 탭합니다.
   
    ![초대 페이지](./media/remoteapp-clients/WinPhone5.png)
6. 초대를 수락하면 액세스할 수 있는 앱 목록이 장치에 다운로드되며 연결 센터에서 사용할 수 있습니다. 앱 중 하나를 탭하여 시작하고 사용합니다.
   
    ![피드가 포함된 연결 센터](./media/remoteapp-clients/WinPhone6.png)
7. 아직 초대가 없는 경우에도 서비스를 체험할 수 있습니다. 이렇게 하려면 메시지가 표시될 때 **예** 를 탭합니다.
   
    ![데모 피드 프롬프트](./media/remoteapp-clients/WinPhone7.png)
8. 이 경우 RemoteApp을 시작하기 위한 기본적인 앱 집합에 액세스할 수 있습니다.
   
    ![Azure RemoteApp에 대한 데모 피드](./media/remoteapp-clients/WinPhone8.png)

