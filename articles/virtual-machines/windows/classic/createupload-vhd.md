---
title: "Powershell을 사용 하 여 aaaCreate 및 업로드 VM 이미지 | Microsoft Docs"
description: "Toocreate 알아보고 hello 클래식 배포 모델 및 Azure Powershell을 사용 하 여 일반화 된 Windows Server 이미지 (VHD)를 업로드 합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>만들기 및 Windows Server VHD tooAzure 업로드
이 문서에서는 어떻게 tooupload 일반화 된 VM 이미지는 가상 하드 디스크 (VHD) toocreate 가상 컴퓨터를 사용할 수 있습니다. Microsoft Azure의 디스크 및 VHD에 대한 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD에 대하여](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.

> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 수도 있습니다 [업로드](../upload-generalized-managed.md) hello 리소스 관리자 모델을 사용 하 여 가상 컴퓨터.

## <a name="prerequisites"></a>필수 조건
이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.

* **Azure 구독** - 계정이 없는 경우 [무료로 Azure 계정을 개설할 수 있습니다](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -있는 hello Microsoft Azure PowerShell 모듈 설치 및 toouse 구독을 구성 합니다.
* **A입니다. VHD 파일** -지원 되는 Windows 운영 체제에서는.vhd 파일 및 연결 된 tooa 가상 컴퓨터에 저장 합니다. Hello 서버 역할 hello VHD에서 실행 되는 Sysprep에서 지원 되는 경우 toosee를 확인 합니다. 자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.

    > [!IMPORTANT]
    > hello VHDX 형식은 Microsoft Azure에서 지원 되지 않습니다. Hyper-v 관리자 또는 hello를 사용 하 여 hello 디스크 tooVHD 형식으로 변환할 수 있습니다 [CONVERT-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx)합니다. 자세한 내용은 이 [블로그 게시물](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx)을 참조하세요.

## <a name="step-1-prep-hello-vhd"></a>1 단계: 준비 hello VHD
Hello VHD tooAzure를 업로드 하기 전에 toobe hello Sysprep 도구를 사용 하 여 이미지를 일반화 해야 합니다. 이미지 형식으로 사용 되는 hello VHD toobe를 준비 합니다. Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다. Sysprep를 실행 하기 전에 hello VM 백업 합니다.

운영 체제 hello hello 가상 컴퓨터에서 절차를 수행 하는 hello를 완료 하려면 설치 됨:

1. Toohello 운영 체제에 로그인 합니다.
2. 관리자로 명령 프롬프트 창을 엽니다. Hello 디렉터리도 변경**%windir%\system32\sysprep**, 한 다음 실행 `sysprep.exe`합니다.

    ![명령 프롬프트 창 열기](./media/createupload-vhd/sysprep_commandprompt.png)
3. hello **시스템 준비 도구** 대화 상자가 나타납니다.

   ![Sysprep 시작](./media/createupload-vhd/sysprepgeneral.png)
4. Hello에 **시스템 준비 도구**선택, **입력 시스템의 상자 경험 OOBE ()** 되어 있는지 확인 **일반화** 을 선택 합니다.
5. **종료 옵션**에서 **종료**를 선택합니다.
6. **확인**을 클릭합니다.

## <a name="step-2-create-a-storage-account-and-a-container"></a>2단계: 저장소 계정 및 컨테이너 만들기
위치 tooupload hello.vhd 파일의 이름을 갖도록 해야 Azure의 저장소 계정. 이 단계를 보면 어떻게 toocreate 계정 또는 get hello 정보에서 기존 계정을 사용 해야 합니다. Hello 변수에서 대체 &lsaquo; 대괄호 &rsaquo; 사용자의 정보로 합니다.

1. 로그인

    ```powershell
    Add-AzureAccount
    ```

2. Azure 구독을 설정합니다.

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. 새 저장소 계정을 만듭니다. hello 저장소 계정의 hello 이름은 고유 해야 합니다. 3-24 자일 합니다. hello 이름에는 문자와 숫자의 조합일 수 있습니다. 또한 toospecify "East US"와 같은 위치를 해야

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. Hello 기본값으로 hello 새 저장소 계정을 설정 합니다.

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. 새 컨테이너를 만듭니다.

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>3 단계: hello.vhd 파일 업로드
사용 하 여 hello [Add-azurevhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD입니다.

Hello 이전 단계에서 사용한 hello Azure PowerShell 창에서 형식 hello 다음 명령 및의 hello 변수 바꾸기 &lsaquo; 대괄호 &rsaquo; 사용자의 정보로 합니다.

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>4 단계: 사용자 지정 이미지의 hello 이미지 tooyour 목록 추가
사용 하 여 hello [Add-azurevmimage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) 사용자 지정 이미지의 cmdlet tooadd hello 이미지 toohello 목록입니다.

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>다음 단계
이제 수 [사용자 지정 VM 만들기](createportal.md) 업로드 이미지 hello를 사용 하 여 합니다.
