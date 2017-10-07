---
title: "Windows Azure VM의 이미지 aaaCapture | Microsoft Docs"
description: "Hello 클래식 배포 모델을 사용 하 여 만든 Azure Windows 가상 컴퓨터의 이미지를 캡처하십시오."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Hello 클래식 배포 모델을 사용 하 여 만든 Azure Windows 가상 컴퓨터의 이미지를 캡처하십시오.
> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. Resource Manager 모델 정보는 [Azure에서 일반화된 VM의 관리되는 이미지 캡처](../capture-image-resource.md)를 참조하세요.

이 문서에서는 어떻게 toocapture Windows 이미지 toocreate로 사용할 수 있도록 다른 가상 컴퓨터를 실행 하는 Azure 가상 컴퓨터. 이 이미지에 hello 운영 체제 디스크는 및 모든 데이터 디스크에 toohello 가상 컴퓨터를 연결 합니다. 네트워킹 구성, 까다롭기 때문에 네트워크 구성을 tooset hello hello 이미지를 사용 하는 다른 가상 컴퓨터를 만들 때 포함 되지 않습니다.

Azure 저장소에서 이미지 hello **VM 이미지 (클래식)**, **계산** 모두를 볼 때 나열 되 서비스에 hello Azure 서비스입니다. 이 hello 업로드 한 이미지가 저장 된 같은 위치입니다. 이미지에 대한 자세한 내용은 [가상 컴퓨터 이미지 정보](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json)를 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에
이러한 단계는 이미 Azure 가상 컴퓨터 생성 되었으며 모든 데이터 디스크를 연결까지 포함 하는 hello 운영 체제 구성 가정 합니다. 아직이 hello 내용은 문서 작성 및 hello 가상 컴퓨터 준비 중에 다음을 참조.

* [이미지에서 가상 컴퓨터 만들기](createportal.md)
* [어떻게 tooattach 데이터 디스크 tooa 가상 컴퓨터](attach-disk.md)
* Hello 서버 역할 Sysprep로 사용할 수 있는지 확인 합니다. 자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.

> [!WARNING]
> 이 프로세스는 캡처된 후 hello 원래 가상 컴퓨터를 삭제 합니다.
>
>

권장 되는 Azure 가상 컴퓨터의 이미지 이전 toocapturing hello 대상 가상 컴퓨터를 백업 합니다. Azure 백업을 사용하여 Azure 가상 컴퓨터를 백업할 수 있습니다. 자세한 내용은 [Azure 가상 컴퓨터 백업](../../../backup/backup-azure-vms.md)을 참조하세요. 다른 솔루션은 인증된 파트너에서 사용할 수 있습니다. 현재 사용할 수 있는 항목을 toofind hello Azure 마켓플레이스를 검색 합니다.

## <a name="capture-hello-virtual-machine"></a>Hello 가상 컴퓨터 캡처
1. Hello에 [Azure 포털](http://portal.azure.com), **연결** toohello 가상 컴퓨터. 자세한 내용은 [어떻게 toosign Windows Server를 실행 하는 tooa 가상 컴퓨터에서][How toosign in tooa virtual machine running Windows Server]합니다.
2. 관리자로 명령 프롬프트 창을 엽니다.
3. Hello 디렉터리도 변경`%windir%\system32\sysprep`, 한 다음 sysprep.exe를 실행 합니다.
4. hello **시스템 준비 도구** 대화 상자가 나타납니다. 다음 hello지 않습니다.

   * **시스템 정리 작업**에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화**를 선택했는지 확인합니다. Sysprep를 사용 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooUse Sysprep: 소개][How tooUse Sysprep: An Introduction]합니다.
   * **종료 옵션**에서 **종료**를 선택합니다.
   * **확인**을 클릭합니다.

   ![Sysprep 실행](./media/capture-image/SysprepGeneral.png)
5. Sysprep 쪽 hello Azure 포털에서에서 가상 컴퓨터 hello의 hello 상태를 변경 하는 hello 가상 컴퓨터 종료**Stopped**합니다.
6. Hello Azure 포털에서에서 클릭 **가상 컴퓨터 (클래식)** 선택 hello toocapture 가상 컴퓨터 및 합니다. hello **VM 이미지 (클래식)** 그룹 아래에 있는지 **계산** 볼 때 **더 많은 서비스**합니다.

7. Hello 명령 모음에서 **캡처**합니다.

   ![가상 컴퓨터 캡처](./media/capture-image/CaptureVM.png)

   hello **가상 컴퓨터 캡처 hello** 대화 상자가 나타납니다.

8. **이미지 이름**를 hello 새 이미지의 이름을 입력 합니다. **이미지 레이블**를 hello 새 이미지에 대 한 레이블을 입력 합니다.

9. 클릭 **hello 가상 컴퓨터에서 Sysprep을 실행 했습니다**합니다. 이 확인란을 3-5 단계에서 Sysprep 사용 하 여 toohello 동작을 의미합니다. 이미지 _해야_ Sysprep을 실행 하는 Windows 서버를 추가 하기 전에 이미지 tooyour 집합이 사용자 지정 이미지를 일반화 합니다.

10. Hello 캡처 완료 되 면 hello 새 이미지에서에서 사용할 수 있게 hello **마켓플레이스**, hello에 **계산**, **VM 이미지 (클래식)** 컨테이너입니다.

    ![이미지 캡처 성공](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>다음 단계
hello 이미지는 사용 되는 준비 toobe toocreate 가상 컴퓨터입니다. toodo이 hello를 선택 하 여 가상 컴퓨터를 만들어 **더 많은 서비스** hello 서비스 메뉴에서 다음의 hello 맨 아래에 있는 메뉴 항목 **VM 이미지 (클래식)** hello에 **계산**그룹입니다. 지침에 대해서는 [이미지에서 가상 컴퓨터 만들기](createportal.md)를 참조하세요.

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
