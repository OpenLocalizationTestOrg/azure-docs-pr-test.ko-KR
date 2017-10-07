---
title: "VHD aaaUpload tooAzure DevTest Labs PowerShell을 사용 하 여 파일 | Microsoft Docs"
description: "PowerShell을 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드"
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a>PowerShell을 사용 하 여 VHD 파일 toolab 저장소 계정에 업로드

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

Azure DevTest Labs, VHD 파일 tooprovision 사용 되는 가상 컴퓨터는 사용자 지정 이미지를 사용 하는 toocreate 될 수 있습니다. hello 다음 단계에 관한 tooupload PowerShell을 사용 하 여 VHD 파일 tooa lab의 저장소 계정입니다. VHD 파일을 업로드 한 후 hello [다음 단계 섹션](#next-steps) toocreate hello에서 사용자 지정 이미지를 VHD 파일을 업로드 하는 방법을 보여 주는 몇 가지 기사를 나열 합니다. Azure의 디스크 및 VHD에 대한 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD 정보](../virtual-machines/linux/about-disks-and-vhds.md)를 참조하세요.

## <a name="step-by-step-instructions"></a>단계별 지침

hello 다음 워크 tooAzure DevTest Labs PowerShell을 사용 하 여 파일을 VHD를 업로드 하는 과정을 안내 합니다. 

1. Toohello 로그인 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040)합니다.

1. 선택 **더 많은 서비스**를 선택한 후 **DevTest Labs** hello 목록에서 합니다.

1. 랩의 hello 목록에서 원하는 랩 hello를 선택 합니다.  

1. Hello 랩 블레이드에서 선택 **구성**합니다. 

1. Hello 랩에 **구성** 블레이드를 **사용자 지정 이미지 (Vhd)**합니다.

1. Hello에 **사용자 지정 이미지** 블레이드에서 선택 **+ 추가**합니다. 

1. Hello에 **사용자 지정 이미지** 블레이드를 **VHD**합니다.

1. Hello에 **VHD** 블레이드를 **PowerShell을 사용 하 여 VHD 업로드**합니다.

    ![PowerShell을 사용하여 VHD 업로드](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. Hello에 **PowerShell을 사용 하 여 이미지를 업로드** 복사 hello 생성 된 PowerShell 스크립트 tooa 텍스트 편집기, 블레이드입니다.

1. Hello 수정 **LocalFilePath** hello의 매개 변수 **Add-azurevhd** hello tooupload VHD 파일의 cmdlet toopoint toohello 위치입니다.

1. PowerShell 프롬프트에서 실행 hello **Add-azurevhd** cmdlet (수정 hello로 **LocalFilePath** 매개 변수).

> [!WARNING] 
> 
> VHD 파일을 업로드할 hello 프로세스 hello VHD 파일의 hello 크기 및 연결 속도 따라 시간이 오래 걸릴 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Hello Azure 포털을 사용 하 여 VHD 파일에서 DevTest Labs를 Azure에서 사용자 지정 이미지 만들기](devtest-lab-create-template.md)
- [PowerShell을 사용하여 VHD 파일에서 Azure DevTest Labs에 사용자 지정 이미지 만들기](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
