---
title: "Azure에서 Linux VHD aaaDownload | Microsoft Docs"
description: "Hello Azure CLI를 사용 하 여 Linux VHD를 다운로드 하 고 hello Azure 포털."
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
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Azure에서 Linux VHD 다운로드

이 문서에서는 설명 어떻게 toodownload는 [Linux 가상 하드 디스크 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure CLI 및 Azure 포털에서 사용 하 여 Azure 파일 hello 합니다. 

사용 하 여 Azure에서 가상 컴퓨터 (Vm) [디스크](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 장소 toostore 운영 체제, 응용 프로그램 및 데이터입니다. 모든 Azure VM은 Windows 운영 체제 디스크와 임시 디스크라는 적어도 2개의 디스크를 갖습니다. 처음 hello 운영 체제 디스크는 이미지에서 생성 하 고 hello 운영 체제 디스크와 hello 이미지는 Vhd는 Azure 저장소 계정에 저장 합니다. 가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다.

아직 수행하지 않았다면 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)을 설치합니다.

## <a name="stop-hello-vm"></a>Hello VM 중지

연결 되어 있는 경우 Azure에서 VHD를 다운로드할 수 없는 tooa VM을 실행 합니다. Toostop hello VM toodownload VHD 필요합니다. Toouse로 VHD를 원하는 경우는 [이미지](tutorial-custom-images.md) toocreate 다른 Vm 새 디스크로 toodeprovision 필요 하 고이 hello에 포함 된 hello 운영 체제를 일반화 파일 및 hello VM을 중지 합니다. toouse hello VHD에 대 한 기존 VM 또는 데이터 디스크의 새 인스턴스를 디스크로 toostop 및 해야 hello VM 할당을 취소 합니다.

toouse 다른 Vm VHD 이미지 toocreate로 hello 다음이 단계를 완료 합니다.

1. SSH, hello 계정 이름 및 hello hello VM tooconnect tooit 공용 IP 주소 사용 하며 프로 비전 해제 해야 합니다. 안녕하세요 + 사용자 매개 변수는 또한 hello 마지막 프로 비전 된 사용자 계정을 제거 합니다. Toohello VM에에서 계정 자격 증명, 동작 하는 경우이 생략 + user 매개 변수입니다. hello 다음 예제에서는 hello 마지막 프로 비전 된 사용자 계정을 제거 합니다.

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Tooyour 된 Azure 계정 로그인 [az 로그인](https://docs.microsoft.com/cli/azure/#login)합니다.
3. 중지 하 고 hello VM 할당을 취소 합니다.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Hello VM을 일반화 합니다. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

toouse hello VHD를 디스크로 기존 VM 또는 데이터 디스크의 새 인스턴스를 다음이 단계를 완료 합니다.

1.  Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2.  Hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다.
3.  Hello VM hello 목록에서 선택 합니다.
4.  Hello VM에 대 한 hello 블레이드에서 클릭 **중지**합니다.

    ![VM 중지](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>SAS URL 생성

toogenerate 해야 toodownload hello VHD 파일에는 [공유 액세스 서명 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL입니다. Hello URL 생성 될 때 만료 시간 toohello URL이 할당 됩니다.

1.  Hello VM에 대 한 hello 블레이드의 hello 메뉴를 클릭 **디스크**합니다.
2.  VM hello에 대 한 hello 운영 체제 디스크를 선택한 다음 클릭 **내보내기**합니다.
3.  **URL 생성**을 클릭합니다.

    ![URL 생성](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>VHD 다운로드

1.  생성 된 hello URL에서 다운로드 hello VHD 파일을 클릭 합니다.

    ![VHD 다운로드](./media/download-vhd/export-download.png)

2.  Tooclick 할 수 있습니다 **저장** hello 브라우저 toostart hello 다운로드에서 합니다. hello VHD 파일에 대 한 기본 이름은 hello *abcd*합니다.

    ![Hello 브라우저에서 저장을 클릭 합니다.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>다음 단계

- 너무 방법에 대해 알아봅니다[업로드 하 고 Azure CLI 2.0 hello로 사용자 지정 디스크에서 Linux VM을 만들](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 
- [Azure 디스크 hello Azure CLI 관리](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

