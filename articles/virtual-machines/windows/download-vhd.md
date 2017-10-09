---
title: "Azure에서 Windows VHD aaaDownload | Microsoft Docs"
description: "Hello Azure 포털을 사용 하 여 Windows VHD를 다운로드 합니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>Azure에서 Windows VHD 다운로드

이 문서에서는 설명 어떻게 toodownload는 [Windows 가상 하드 디스크 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 사용 하 여 Azure에서 파일 hello Azure 포털입니다. 

사용 하 여 Azure에서 가상 컴퓨터 (Vm) [디스크](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 장소 toostore 운영 체제, 응용 프로그램 및 데이터입니다. 모든 Azure VM은 Windows 운영 체제 디스크와 임시 디스크라는 적어도 2개의 디스크를 갖습니다. 처음 hello 운영 체제 디스크는 이미지에서 생성 하 고 hello 운영 체제 디스크와 hello 이미지는 Vhd는 Azure 저장소 계정에 저장 합니다. 가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.

## <a name="stop-hello-vm"></a>Hello VM 중지

연결 되어 있는 경우 Azure에서 VHD를 다운로드할 수 없는 tooa VM을 실행 합니다. Toostop hello VM toodownload VHD 필요합니다. Toouse로 VHD를 원하는 경우는 [이미지](tutorial-custom-images.md) toocreate 사용 하면 새 디스크와 다른 Vm에 [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello 파일에 포함 된 운영 체제 hello 및 hello VM을 중지 합니다. toouse hello VHD에 대 한 기존 VM 또는 데이터 디스크의 새 인스턴스를 디스크로 toostop 및 해야 hello VM 할당을 취소 합니다.

toouse 다른 Vm VHD 이미지 toocreate로 hello 다음이 단계를 완료 합니다.

1.  그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2.  [Toohello VM 연결](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 
3.  Hello VM에서 관리자 권한으로 명령 프롬프트 창을 hello를 엽니다.
4.  Hello 디렉터리도 변경*%windir%\system32\sysprep* sysprep.exe를 실행 합니다.
5.  Hello 시스템 준비 도구 대화 상자에서 선택 **입력 시스템을 기본 OOBE (Experience)**, 있는지 확인 하 고 **일반화** 을 선택 합니다.
6.  종료 옵션에서 **종료**를 선택한 다음 **확인**을 클릭합니다. 

toouse hello VHD를 디스크로 기존 VM 또는 데이터 디스크의 새 인스턴스를 다음이 단계를 완료 합니다.

1.  Hello Azure 포털에서에서 hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다.
2.  Hello VM hello 목록에서 선택 합니다.
3.  Hello VM에 대 한 hello 블레이드에서 클릭 **중지**합니다.

    ![VM 중지](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>SAS URL 생성

toogenerate 해야 toodownload hello VHD 파일에는 [공유 액세스 서명 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL입니다. Hello URL 생성 될 때 만료 시간 toohello URL이 할당 됩니다.

1.  Hello VM에 대 한 hello 블레이드의 hello 메뉴를 클릭 **디스크**합니다.
2.  VM hello에 대 한 hello 운영 체제 디스크를 선택한 다음 클릭 **내보내기**합니다.
3.  Hello URL의 hello 만료 시간을 너무 설정*36000*합니다.
4.  **URL 생성**을 클릭합니다.

    ![URL 생성](./media/download-vhd/export-generate.png)

> [!NOTE]
> hello 만료 시간 toodownload hello 큰 VHD 파일에서 Windows Server 운영 체제에 대 한 충분 한 시간 hello 기본 tooprovide에서 증가 되었습니다. Windows Server 운영 체제 tootake hello 연결 방식에 따라 몇 시간 toodownload를 포함 하는 VHD 파일을 기대할 수 있습니다. 데이터 디스크에 대 한 VHD를 다운로드 하는 경우 hello 기본 시간은 충분 한입니다. 
> 
> 

## <a name="download-vhd"></a>VHD 다운로드

1.  생성 된 hello URL에서 다운로드 hello VHD 파일을 클릭 합니다.

    ![VHD 다운로드](./media/download-vhd/export-download.png)

2.  Tooclick 할 수 있습니다 **저장** hello 브라우저 toostart hello 다운로드에서 합니다. hello VHD 파일에 대 한 기본 이름은 hello *abcd*합니다.

    ![Hello 브라우저에서 저장을 클릭 합니다.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>다음 단계

- 너무 방법에 대해 알아봅니다[업로드할 VHD 파일 tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 
- [저장소 계정의 비관리 디스크에서 관리 디스크를 만듭니다](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- [PowerShell을 사용하여 Azure 디스크를 관리합니다](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

