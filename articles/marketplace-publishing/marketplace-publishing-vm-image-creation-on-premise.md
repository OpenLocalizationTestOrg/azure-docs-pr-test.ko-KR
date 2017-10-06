---
title: "Azure 마켓플레이스 hello에 대 한 온-프레미스 가상 컴퓨터 이미지 aaaCreating | Microsoft Docs"
description: "이해 및 hello 단계 toocreate 온-프레미스 VM 이미지를 실행 하 고 다른 사용자에 대 한 Azure 마켓플레이스 toohello 배포 toopurchase 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>Azure 마켓플레이스 hello에 대 한 온-프레미스 가상 컴퓨터 이미지를 개발 합니다.
원격 데스크톱 프로토콜을 사용 하 여 hello 클라우드에서 직접 Azure 가상 하드 디스크 (Vhd)를 개발 하는 것이 좋습니다. 그러나 필요한 경우 가능한 toodownload VHD 이며 온-프레미스 인프라를 사용 하 여 개발 합니다.  

온-프레미스 개발의 경우 hello 운영 체제의 hello 만든 VHD를 다운로드 해야 VM입니다. 다음 단계는 위의 3.3단계의 일부로 수행됩니다.  

## <a name="download-a-vhd-image"></a>VHD 이미지 다운로드
### <a name="locate-a-blob-url"></a>Blob URL 찾기
순서 toodownload hello VHD에서 먼저 hello 운영 체제 디스크에 대 한 hello blob URL를 찾습니다.

새 hello에서 hello blob URL을 찾을 [Microsoft Azure 포털](https://portal.azure.com):

1. 너무 이동**찾아보기** > **Vm**를 선택한 후 hello VM을 배포 합니다.
2. **구성**선택, hello **디스크** 타일을 hello 디스크 블레이드가 열립니다.
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. 선택 hello **OS 디스크**, hello VHD 위치를 포함 하 여 디스크 속성을 표시 하는 다른 블레이드가 열립니다.
4. 이 Blob URL을 복사합니다.
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. 이제 삭제 hello hello 백업 디스크를 삭제 하지 않고 VM을 배포 합니다. 삭제 하는 대신 hello VM을 중지할 수도 있습니다. Hello VM에서 실행 중인 경우에 hello 운영 체제 VHD를 다운로드 하지 마십시오.
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>VHD 다운로드
Hello blob URL을 알고 있다면 후 hello를 사용 하 여 hello VHD를 다운로드할 수 있습니다 [Azure 포털](http://manage.windowsazure.com/) 또는 PowerShell입니다.  

> [!NOTE]
> 이 가이드의이 만들기의 hello 시 hello 기능 toodownload VHD 아직 없으면 hello 새 Microsoft Azure 포털에서 합니다.  
> 
> 

**현재 hello 통해 hello 운영 체제 VHD 다운로드 [Azure 포털](http://manage.windowsazure.com/)**

1. 하지 않았으면 지금 이미 경우 toohello Azure 포털에에서 로그인 합니다.
2. Hello 클릭 **저장소** 탭 합니다.
3. 저장 된 VHD는 hello 내 hello 저장소 계정을 선택 합니다.
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. 그러면 저장소 계정 속성이 표시됩니다. 선택 hello **컨테이너** 탭 합니다.
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. hello에 VHD 저장 되는 hello 컨테이너를 선택 합니다. 기본적으로 hello 포털에서 만든 VHD hello vhd 컨테이너에 저장 됩니다.
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Hello URL toohello 저장 하나 비교 하 여 hello 올바른 운영 체제 VHD를 선택 합니다.
7. **다운로드**를 클릭합니다.
   
   ![그리기](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>PowerShell을 사용하여 VHD 다운로드
또한 toousing hello Azure 포털, hello를 사용할 수 있습니다 [Save-azurevhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello 운영 체제 VHD입니다.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
예: Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String>

> [!NOTE]
> **Save-azurevhd** 역시는 **NumberOfThreads** 수 있는 옵션이 hello 다운로드용 tooincrease 병렬 처리 수준 toomake hello 사용에 가장 적합 사용 가능한 대역폭을 사용 합니다.
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>Vhd tooan Azure 저장소 계정에 업로드
Vhd 온-프레미스를 준비 해야 tooupload 저장소로 azure에서 계정. 이 단계는 온-프레미스에서 VHD를 만든 후, VM 이미지에 대한 인증을 가져오기 전에 수행됩니다.

### <a name="create-a-storage-account-and-container"></a>저장소 계정 및 컨테이너 만들기
Hello 미국에 있는 영역에서 저장소 계정에 Vhd를 업로드 하는 것이 좋습니다. 단일 SKU에 대한 모든 VHD는 단일 저장소 계정 내에서 단일 컨테이너에 배치되어야 합니다.

저장소 계정 toocreate hello를 사용할 수 있습니다 [Microsoft Azure 포털](https://portal.azure.com/), PowerShell 또는 hello Linux 명령줄 도구입니다.  

**Hello Microsoft Azure 포털에서 저장소 계정을 만들려면**

1. **새로 만들기**를 클릭합니다.
2. **저장소**를 선택합니다.
3. Hello 저장소 계정 이름에 채운 다음 위치를 선택 합니다.
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. **만들기**를 클릭합니다.
5. 저장소 계정을 만든 hello에 대 한 hello 블레이드 열려 있어야 합니다. 그렇지 않은 경우 **찾아보기** > **저장소 계정**을 선택합니다. 계정 블레이드 hello 저장소에서 만든 hello 저장소 계정을 선택 합니다.
6. **컨테이너**를 선택합니다.
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. Hello 컨테이너 블레이드에서 선택 **추가**를 컨테이너 이름 및 hello 컨테이너 권한을 입력 합니다. 컨테이너 권한에 대해 **개인** 을 선택합니다.

> [!TIP]
> Toopublish를 계획 하는 SKU 당 하나의 컨테이너를 만들어야 하는 것이 좋습니다.
> 
> 

  ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>PowerShell을 사용하여 저장소 계정 만들기
Hello를 사용 하 여 저장소 계정을 만드는 PowerShell을 사용 하 여 [새로 AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

그러면 hello를 사용 하 여 해당 저장소 계정 내의 컨테이너를 만들 수 있습니다 [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> 이러한 명령이 PowerShell에서 이미 설정 되어 해당 hello 현재 저장소 계정 컨텍스트를 가정 합니다.   너무 참조[Azure PowerShell을 설정](marketplace-publishing-powershell-setup.md) PowerShell 설치에 대 한 자세한 내용은 합니다.  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>Mac 및 Linux 용 hello 명령줄 도구를 사용 하 여 저장소 계정 만들기
> [Linux 명령줄 도구](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 다음과 같이 저장소 계정을 만듭니다.
> 
> 

        azure storage account create mystorageaccount --location "West US"

다음과 같이 컨테이너를 만듭니다.

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>VHD 업로드
Hello 저장소 계정 및 컨테이너를 만든 후에 준비 된 Vhd를 업로드할 수 있습니다. PowerShell, hello Linux 명령줄 도구 또는 기타 Azure 저장소 관리 도구를 사용할 수 있습니다.

### <a name="upload-a-vhd-via-powershell"></a>PowerShell 통해 VHD 업로드
사용 하 여 hello [Add-azurevhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>Mac 및 Linux 용 hello 명령줄 도구를 사용 하 여 VHD 업로드
Hello로 [Linux 명령줄 도구](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), hello 다음 이름을 사용해 서: azure vm 이미지 만들기 <image name> -위치 <Location of hello data center> -OS Linux<LocationOfLocalVHD>

## <a name="see-also"></a>참고 항목
* [마켓플레이스 hello에 대 한 가상 컴퓨터 이미지 만들기](marketplace-publishing-vm-image-creation.md)
* [Azure PowerShell 설정](marketplace-publishing-powershell-setup.md)

