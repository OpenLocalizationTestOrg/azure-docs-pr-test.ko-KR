---
title: "Azure VM을 기반으로 Azure RemoteApp 이미지 만들기 | Microsoft 문서"
description: "Azure 가상 컴퓨터를 시작하여 Azure RemoteApp에 대한 이미지를 만드는 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ee64b86835af8e6237cddcd8acc779fc6dac8214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Azure 가상 컴퓨터를 기반으로 Azure RemoteApp 이미지 만들기
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.
> 
> 

Azure 가상 컴퓨터에서 Azure RemoteApp 이미지(컬렉션에서 공유하는 앱을 포함)를 만들 수 있습니다. Azure RemoteApp 이미지 요구 사항을 모두 충족하는 Azure VM 이미지 갤러리에 추가한 가상 컴퓨터 이미지를 사용하도록 선택할 수도 있습니다. 원하는 경우 해당 VM 이미지를 자신만의 VM을 위한 시작점으로 사용할 수 있습니다. "Windows Server 원격 데스크톱 세션 호스트" 이미지를 라이브러리에서 찾으면 됩니다.

Azure VM을 기반으로 자신만의 이미지를 만드는 단계는 두 가지입니다. 이미지를 만든 다음 Azure VM 라이브러리에서 Azure RemoteApp으로 업로드하는 것입니다.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Azure VM을 기반으로 사용자 지정 이미지 만들기
Azure VM을 기반으로 이미지를 만들려면 이 단계를 사용합니다.

1. Azure 가상 컴퓨터를 만듭니다. Azure 가상 컴퓨터 이미지 갤러리에서 "Windows Server 원격 데스크톱 세션 호스트" 또는 "Microsoft Office 365 ProPlus가 있는 Windows Server 원격 데스크톱 세션 호스트" 이미지를 사용할 수 있습니다. 이 이미지는 Azure RemoteApp 템플릿 이미지 요구 사항을 모두 충족합니다.
   
    자세한 내용은 [Windows를 실행하는 VM 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.
2. VM에 연결하고 RemoteApp을 통해 공유하려는 앱을 구성합니다. 앱에 필요한 모든 추가 Windows 구성을 수행할 수 있는지 확인합니다.
   
    자세한 내용은 [Windows Server를 실행하는 가상 컴퓨터에 로그온하는 방법](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.
3. Windows Server 원격 데스크톱 세션 호스트 이미지 중 하나를 사용하는 경우 VM이 RemoteApp 사전 요구 사항을 충족하는지 확인하는 유효성 검사 스크립트가 포함되어 있습니다. 스크립트를 실행하려면 바탕 화면에서 **ValidateRemoteAppImage** 를 두 번 클릭합니다. 다음 단계를 진행하기 전에 스크립트에서 보고한 모든 오류가 해결되었는지 확인합니다.
4. SYSPREP가 일반화되고 이미지를 캡처합니다. 지침에 대해서는 [템플릿으로 사용할 Windows Virtual Machine를 캡처하는 방법](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.

## <a name="import-the-image-into-the-azure-remoteapp-image-library"></a>Azure RemoteApp 이미지 라이브러리로 이미지 가져오기
다음 단계를 사용하여 새 이미지를 Azure RemoteApp으로 가져옵니다.

1. **템플릿 이미지** 탭에서 다음을 수행합니다.
   
   * 기존 이미지가 없는 경우 **템플릿 이미지를 업로드하거나 가져오기**를 클릭합니다.
   * 하나 이상의 이미지가 이미 있는 경우 **+** 를 클릭하여 새 이미지를 추가합니다.
2. **Virtual Machines에서 이미지 가져오기** 라이브러리를 선택한 후 **다음**을 클릭합니다.
3. 다음 페이지에서 목록에서 사용자 지정 이미지를 선택하고 이미지를 만들 때 나열된 단계를 수행했는지 확인합니다. **다음**을 누릅니다.
4. 새 RemoteApp 이미지에 대한 이름을 입력하고 위치를 선택한 다음 확인 표시를 클릭하여 가져오기 프로세스를 시작합니다.

> [!NOTE]
> Azure 가상 컴퓨터에서 지원하는 모든 Azure 위치에서 Azure RemoteApp에서 지원하는 모든 Azure 위치로 이미지를 가져올 수 있습니다. 가져오기는 위치에 따라 최대 25분까지 걸릴 수 있습니다.
> 
> 

이제 필요에 따라 [클라우드](remoteapp-create-cloud-deployment.md) 컬렉션 또는 [하이브리드](remoteapp-create-hybrid-deployment.md), 컬렉션을 새로 만들 준비가 되었습니다.

