---
title: "Azure 역할과 함께 원격 데스크톱 사용 | Microsoft Docs"
description: "Azure 역할과 함께 원격 데스크톱 사용"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: eab135d10c0d6df8ca72ac47d6804017a998a3d2
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a>Azure 역할과 함께 원격 데스크톱 사용
Azure SDK와 원격 데스크톱 서비스를 사용하여 Azure 역할 및 Azure에서 호스팅되는 가상 컴퓨터에 액세스할 수 있습니다. Visual Studio에서 Azure 클라우드 서비스 프로젝트에서 원격 데스크톱 서비스를 구성할 수 있습니다. 원격 데스크톱 서비스를 사용하려면 하나 이상의 역할을 포함하는 작업 프로젝트를 만든 다음 Azure에 게시합니다.

> [!IMPORTANT]
> 문제 해결 또는 개발 목적으로만 Azure 역할에 액세스해야 합니다. 각 가상 컴퓨터는 다른 클라이언트 응용 프로그램이 아닌 Azure 응용 프로그램에서 특정 역할을 실행하고자 합니다. Azure를 사용하여 어떤 목적으로든 사용할 수 있는 가상 컴퓨터를 호스트하려면, 서버 탐색기에서 Azure 가상 컴퓨터에 액세스를 참조하세요.
> 
> 

## <a name="to-enable-and-use-remote-desktop-for-an-azure-role"></a>Azure 역할에 대한 원격 데스크톱을 사용하려면
1. 솔루션 탐색기에서 클라우드 서비스 프로젝트에 대한 바로 가기 메뉴를 열고 **게시**를 선택합니다.
   
    **Azure 응용 프로그램 게시** 마법사가 나타납니다.
   
    ![클라우드 서비스 프로젝트에 대한 명령 게시](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. 마법사의 **Microsoft Azure 게시 설정** 페이지 아래쪽에서 모든 역할에 대해 **원격 데스크톱 사용** 확인란을 선택합니다. 
   
    **원격 데스크톱 구성** 대화 상자가 나타납니다.
3. **원격 데스크톱 구성** 대화 상자의 아래쪽에서 **기타 옵션** 단추를 선택합니다. 
   
    원격 데스크톱을 통해 연결 시 자격 증명 정보를 암호화할 수 있도록 인증서를 만들거나 선택할 수 있는 드롭다운 목록 상자를 표시합니다.
4. 드롭다운 목록에서 **&lt;만들기>**를 선택하거나 목록에서 기존 항목을 선택합니다. 
   
    기존 인증서를 선택하면 다음 단계를 건너뜁니다.
   
   > [!NOTE]
   > 원격 데스크톱 연결에 필요한 인증서는 다른 Azure 작업에 사용하는 인증서와 다릅니다. 원격 액세스 인증서에는 개인 키가 있어야 합니다.
   > 
   > 
   
    **인증서 만들기** 대화 상자가 나타납니다.
   
   1. 새 인증서에 대해 친숙한 이름을 입력한 다음 **확인** 단추를 선택합니다. 새 인증서가 드롭다운 목록 상자에 나타납니다.
   2. **원격 데스크톱 구성** 대화 상자에 사용자 이름 및 암호를 입력합니다.
      
       기존 계정을 사용할 수 없습니다. 관리자를 새 계정에 대한 사용자 이름으로 지정하지 않습니다.
      
      > [!NOTE]
      > 암호가 복잡성 요구 사항을 충족하지 않는 경우, 암호 텍스트 상자 옆에 빨간색 아이콘이 나타납니다. 암호는 대문자, 소문자 및 숫자나 기호를 포함해야 합니다.
      > 
      > 
   3. 계정이 만료될 날짜 및 차단될 원격 데스크톱 연결을 선택합니다.
   4. 필요한 모든 정보를 입력한 후 **확인** 단추를 선택합니다.
      
       원격 액세스 서비스를 사용하는 여러 설정이 .cscfg 및 .csdef 파일에 추가됩니다.
5. **Microsoft Azure 게시 설정** 마법사에서 클라우드 서비스를 게시할 준비가 되면 **확인** 단추를 선택합니다.
   
    게시할 준비가 되지 않은 경우 **취소** 단추를 선택합니다. 구성 설정이 저장되고 나중에 클라우드 서비스를 게시할 수 있습니다.

## <a name="connect-to-an-azure-role-by-using-remote-desktop"></a>원격 데스크톱을 사용하여 Azure 역할에 연결
Azure에서 클라우드 서비스를 게시한 후 서버 탐색기를 사용하여 Azure가 호스팅하는 가상 컴퓨터에 로그인할 수 있습니다. 

1. 서버 탐색기에서 **Azure** 노드를 확장한 다음 클라우드 서비스에 대한 노드 및 해당 역할 중 하나를 확장하여 인스턴스 목록을 표시합니다.
2. 인스턴스 노드에 대한 바로 가기 메뉴를 열고 **원격 데스크톱을 사용하여 연결**을 선택합니다.
   
    ![원격 데스크톱을 통해 연결](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. 이전에 만든 사용자 이름 및 암호를 입력합니다. 이제 원격 세션에 로그인됩니다.

