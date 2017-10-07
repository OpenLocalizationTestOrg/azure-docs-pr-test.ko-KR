---
title: "Azure RemoteApp 이미지는 Azure VM에 따라 aaaCreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Azure 가상 컴퓨터를 시작 하 여 Azure RemoteApp에 대 한 이미지입니다."
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
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Azure 가상 컴퓨터를 기반으로 Azure RemoteApp 이미지 만들기
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure 가상 컴퓨터에서 Azure RemoteApp 이미지 (보존 하는 사용자의 컬렉션에서 공유 하는 hello 앱)를 만들 수 있습니다. 선택할 수도 있습니다 toouse 모든 hello Azure RemoteApp 이미지 요구 사항에 맞는 toohello Azure VM 이미지 갤러리 추가 가상 컴퓨터 이미지-경우 사용할 수 있습니다 VM 이미지가 시작 지점으로 직접 VM에 대 한 원하는 합니다. Hello "Windows Server 원격 데스크톱 세션 호스트" 이미지 hello 라이브러리를 찾아 보십시오.

사용자 고유의 이미지는 Azure VM에 따라 두 단계 toocreate는-hello 이미지를 만들고 hello Azure VM 라이브러리 tooAzure RemoteApp에서에서 업로드 합니다.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Azure VM을 기반으로 사용자 지정 이미지 만들기
이러한 단계 toocreate Azure VM을 기반으로 이미지를 사용 합니다.

1. Azure 가상 컴퓨터를 만듭니다. Hello Azure 가상 컴퓨터 이미지 갤러리에서 "Windows Server 원격 데스크톱 세션 호스트" hello 또는 hello "Windows Server 원격 데스크톱 세션 호스트와 Microsoft Office 365 ProPlus" 이미지를 사용할 수 있습니다. 이 이미지는 모든 hello Azure RemoteApp 템플릿 이미지 요구를 충족합니다.
   
    자세한 내용은 [Windows를 실행하는 VM 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.
2. VM toohello를 연결 하 고 설치를 통해 RemoteApp tooshare hello 앱을 구성 합니다. 앱에 필요한 추가 Windows 구성이 tooperform 있는지를 확인 합니다.
   
    자세한 내용은 참조 [어떻게 tooLog tooa Windows Server를 실행 하는 가상 컴퓨터에](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.
3. Hello Windows Server 원격 데스크톱 세션 호스트 이미지 중 하나를 사용 하는 경우 VM 충족 hello RemoteApp 사전 reqs. 수 있도록 보장 하는 포함 된 유효성 검사 스크립트 toorun 스크립트를 두 번 클릭 **ValidateRemoteAppImage** hello 바탕 화면에서. Hello 스크립트에서 보고 된 모든 오류 toohello 다음 단계를 진행 하기 전에 해결 된 것을 확인 합니다.
4. SYSPREP /generalize 및 hello 이미지를 캡처합니다. 참조 [어떻게 tooCapture 템플릿으로 Windows 가상 컴퓨터 tooUse](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 지침에 대 한 합니다.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Hello 이미지 hello Azure RemoteApp 이미지 라이브러리에 가져와야 합니다.
이러한 단계 tooimport hello 새 이미지를 사용 하 여 Azure RemoteApp에:

1. Hello에 **템플릿 이미지** 탭:
   
   * 기존 이미지가 없는 경우 **템플릿 이미지를 업로드하거나 가져오기**를 클릭합니다.
   * 하나 이상의 이미지를 이미 있는 경우 클릭  **+**  tooadd 새 이미지입니다.
2. **Virtual Machines에서 이미지 가져오기** 라이브러리를 선택한 후 **다음**을 클릭합니다.
3. Hello 다음 페이지에서 hello 목록에서 사용자 지정 이미지를 선택 하 고 이미지를 만들 때를 나열 된 hello 단계를 수행 했는지 확인 합니다. **다음**을 누릅니다.
4. Hello 새 RemoteApp 이미지에 대 한 이름을 입력 하 고 hello 위치를 선택 하 고 hello 확인 표시 toostart hello 가져오기 프로세스를 클릭 합니다.

> [!NOTE]
> Azure 가상 컴퓨터 tooany Azure RemoteApp에서 지원 되는 Azure 위치에서 지 원하는 모든 Azure 위치에서 이미지를 가져올 수 있습니다. Hello 위치에 따라 hello 가져오기 too25 분와 차지할 수 있습니다.
> 
> 

이제 사용할 수 있는 상태 toocreate 새 컬렉션 중 하나는 [클라우드](remoteapp-create-cloud-deployment.md) 컬렉션 또는 [하이브리드](remoteapp-create-hybrid-deployment.md)필요에 따라 합니다.

