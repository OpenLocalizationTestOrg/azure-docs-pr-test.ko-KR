---
title: "VHD aaaUpload tooAzure DevTest Labs AzCopy를 사용 하 여 파일 | Microsoft Docs"
description: "AzCopy를 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>AzCopy를 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

Azure DevTest Labs, VHD 파일 tooprovision 사용 되는 가상 컴퓨터는 사용자 지정 이미지를 사용 하는 toocreate 될 수 있습니다. 단계를 수행 하는 hello에 관한 AzCopy 명령줄 유틸리티 tooupload hello를 사용 하 여 VHD 파일 tooa lab의 저장소 계정입니다. VHD 파일을 업로드 한 후 hello [다음 단계 섹션](#next-steps) toocreate hello에서 사용자 지정 이미지를 VHD 파일을 업로드 하는 방법을 보여 주는 몇 가지 기사를 나열 합니다. Azure의 디스크 및 VHD에 대한 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD 정보](../virtual-machines/linux/about-disks-and-vhds.md)를 참조하세요.

> [!NOTE] 
>  
> AzCopy는 Windows 전용 명령줄 유틸리티입니다.

## <a name="step-by-step-instructions"></a>단계별 지침

다음 단계 워크 tooAzure DevTest Labs를 사용 하 여 파일을 VHD를 업로드 하는 과정를 hello [AzCopy](http://aka.ms/downloadazcopy)합니다. 

1. Hello hello 랩 저장소 계정의 이름으로 hello Azure 포털을 사용 하 여 가져오기:

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.

1. 선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.

1. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.  

1. Hello 랩 블레이드에서 선택 **구성**합니다. 

1. Hello 랩에 **구성** 블레이드를 **사용자 지정 이미지 (Vhd)**합니다.

1. Hello에 **사용자 지정 이미지** 블레이드에서 선택 **+ 추가**합니다. 

1. Hello에 **사용자 지정 이미지** 블레이드를 **VHD**합니다.

1. Hello에 **VHD** 블레이드를 **PowerShell을 사용 하 여 VHD 업로드**합니다.

    ![PowerShell을 사용하여 VHD 업로드](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. hello **PowerShell을 사용 하 여 이미지를 업로드** 블레이드 표시 호출 toohello **Add-azurevhd** cmdlet. 첫 번째 매개 변수를 hello (*대상*) blob 컨테이너에 대 한 hello URI가 포함 되어 (*업로드*) 형식에 따라 hello에:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Hello 기록 이후 단계에서 사용 중 이므로 완전 한 URI입니다.

1. AzCopy를 사용 하 여 hello VHD 파일을 업로드 합니다.
 
1. [Hello AzCopy의 최신 버전 다운로드 및 설치](http://aka.ms/downloadazcopy)합니다.

1. 명령 창을 열고 toohello AzCopy 설치 디렉터리를 이동 합니다. 필요에 따라 hello AzCopy 설치 위치 tooyour 시스템 경로 추가할 수 있습니다. 기본적으로 AzCopy는 디렉터리를 다음 설치 된 toohello은:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Hello 저장소 계정 키와 blob 컨테이너 URI를 사용 하 여, hello 다음 hello 명령 프롬프트에서 명령을 실행 합니다. hello *vhdFileName* 따옴표로 toobe 필요한 값입니다. VHD 파일을 업로드할 hello 프로세스 hello VHD 파일의 hello 크기 및 연결 속도 따라 시간이 오래 걸릴 수 있습니다.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>다음 단계

- [Hello Azure 포털을 사용 하 여 VHD 파일에서 DevTest Labs를 Azure에서 사용자 지정 이미지 만들기](devtest-lab-create-template.md)
- [PowerShell을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기](devtest-lab-create-custom-image-from-vhd-using-powershell.md)