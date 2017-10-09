---
title: "aaaHow toocreate 관리 또는 hello Azure 포털에서에서 저장소 계정을 삭제 | Microsoft Docs"
description: "새 저장소 계정 만들기, 계정 액세스 키를 관리 또는 hello Azure 포털에서에서 저장소 계정을 삭제 합니다. 표준 및 프리미엄 저장소 계정에 대해 알아봅니다."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 3a2a07c4131fbe594c7007f59950bf94339809fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Azure 저장소 계정 정보
[!INCLUDE [storage-selector-portal-create-storage-account](../../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>개요
Azure 저장소 계정을 고유한 네임 스페이스 toostore 제공 및 Azure 저장소 데이터 개체에 액세스 합니다. 저장소 계정의 모든 개체는 그룹으로 합산 청구됩니다. Hello 계정의 데이터는 기본적으로 사용할 수 있는 유일한 tooyou hello 계정 소유자입니다.

[!INCLUDE [storage-account-types-include](../../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>저장소 계정 사용 비용
[!INCLUDE [storage-account-billing-include](../../../includes/storage-account-billing-include.md)]

> [!NOTE]
> Azure 가상 컴퓨터를 만들 때 저장소 계정 수에 대 한 경우 자동으로 만들어집니다 hello 배포 위치에서 해당 위치에 저장소 계정을 아직 없는 있습니다. 따라서 가상 컴퓨터 디스크에 대 한 저장소 계정 toocreate 아래 필요한 toofollow hello 단계는 없습니다. hello 저장소 계정 이름은 hello 가상 컴퓨터 이름 기반 이어야 합니다. Hello 참조 [Azure 가상 컴퓨터 설명서](https://azure.microsoft.com/documentation/services/virtual-machines/) 내용을 확인 합니다.
> 
> 

## <a name="storage-account-endpoints"></a>저장소 계정 끝점
Azure 저장소에 저장되는 모든 개체에는 고유한 URL 주소가 있습니다. hello 저장소 계정 이름 형식은 hello 해당 주소의 하위 도메인입니다. hello는 특정 tooeach 서비스 하위 도메인 및 도메인 이름 조합이 형성 된 *끝점* 저장소 계정에 대 한 합니다.

예를 들어 저장소 계정의 이름이 *mystorageaccount*, 저장소 계정에 대 한 hello 기본 끝점은 다음:

* Blob 서비스: http://*mystorageaccount*.blob.core.windows.net
* Table service: http://*mystorageaccount*.table.core.windows.net
* 큐 서비스: http://*mystorageaccount*.queue.core.windows.net
* 파일 서비스: http://*mystorageaccount*.file.core.windows.net

> [!NOTE]
> Blob 저장소 계정 hello Blob 서비스 끝점을 노출합니다.
> 
> 

저장소 계정에는 개체에 액세스 하기 위한 hello URL hello 저장소 계정 toohello 끝점에서 hello 개체의 위치를 추가 하 여 만들어집니다. 예를 들어 Blob 주소의 형식은 다음과 같습니다. http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*

사용자 지정 도메인 이름을 toouse 스토리지 계정으로 구성할 수도 있습니다. 자세한 내용은 [Blob Storage 끝점에 대한 사용자 지정 도메인 이름 구성](../blobs/storage-custom-domain-name.md)을 참조하세요. PowerShell에서도 구성할 수 있습니다. 자세한 내용은 참조 hello [집합 AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet.  


## <a name="create-a-storage-account"></a>저장소 계정 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 허브 메뉴에서 선택 **새로** -> **저장소** -> **저장소 계정**합니다.
3. 저장소 계정의 이름을 입력합니다. 참조 [저장소 계정 끝점](#storage-account-endpoints) 에 대 한 자세한 내용을 hello 저장소 계정 이름을 사용 하는 tooaddress 되는 방식을 Azure 저장소의 개체입니다.
   
   > [!NOTE]
   > 저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.
   > 
   > 저장소 계정 이름은 Azure 내에서 고유해야 합니다. Azure 포털 hello 선택한 hello 저장소 계정 이름은 이미 사용 중인지 여부 표시 됩니다.
   > 
   > 
4. Hello 배포 모델 toobe 사용 지정: **리소스 관리자** 또는 **클래식**합니다. **리소스 관리자** hello 배포 모델 좋습니다. 자세한 내용은 [리소스 관리자 배포 및 클래식 배포 이해](../../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.
   
   > [!NOTE]
   > Blob 저장소 계정은 hello 리소스 관리자 배포 모델을 사용 하 여 서만 만들 수 있습니다.

5. Hello 유형의 저장소 계정 선택: **범용** 또는 **Blob 저장소**합니다. **일반 용도의** hello 기본값입니다.
   
    경우 **범용** 을 선택한 다음 hello 성능 계층을 지정: **표준** 또는 **프리미엄**합니다. hello 기본값은 **표준**합니다. 표준 및 프리미엄 저장소 계정에 대 한 자세한 내용은 참조 하십시오. [Azure 저장소 소개 tooMicrosoft](storage-introduction.md) 및 [프리미엄 저장소: Azure 가상 컴퓨터 워크 로드 용 고성능 저장소](storage-premium-storage.md)합니다.
   
    경우 **Blob 저장소** 을 선택한 다음 hello 액세스 계층을 지정: **핫** 또는 **쿨**합니다. hello 기본값은 **핫**합니다. 자세한 내용은 [Azure Blob 저장소: 쿨 및 핫 계층](../blobs/storage-blob-storage-tiers.md) 을 참조하세요.
6. Hello 저장소 계정에 대 한 hello 복제 옵션을 선택: **LRS**, **GRS**, **RA-GRS**, 또는 **ZRS**합니다. hello 기본값은 **RA-GRS**합니다. Azure 저장소 복제 옵션에 대한 자세한 내용은 아래의 [Azure 저장소 복제](storage-redundancy.md)를 참조하세요.
7. Hello 구독 하려는 toocreate hello 새 저장소 계정을 선택 합니다.
8. 새 리소스 그룹을 지정하거나 기존 리소스 그룹을 선택합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md)를 참조하세요.
9. 저장소 계정에 대 한 hello 지리적 위치를 선택 합니다. 각 지역에서 어떤 서비스가 가능한지에 대한 자세한 정보는 [Azure 지역](https://azure.microsoft.com/regions/#services) 을 참조하세요.
10. 클릭 **만들기** toocreate hello 저장소 계정입니다.

## <a name="manage-your-storage-account"></a>저장소 계정 관리
### <a name="change-your-account-configuration"></a>계정 구성 변경
저장소 계정을 만든 후에 hello 계정 또는 Blob 저장소 계정에 대 한 변경 hello 액세스 계층에 사용 되는 hello 복제 옵션을 변경 하는 등의 구성을 수정할 수 있습니다. Hello에 [Azure 포털](https://portal.azure.com), tooyour 저장소 계정, 찾기 및 클릭 탐색 **구성** 아래 **설정을** hello 계정 구성을 tooview 및/또는 변경 합니다.

> [!NOTE]
> Hello 저장소 계정을 만들 때 선택한 hello 성능 계층에 따라 일부 복제 옵션을 사용 하지 못할 수 있습니다.
> 
> 

Hello 복제 옵션을 변경 하면 가격 변경 됩니다. 자세한 내용은 [Azure 저장소 가격 책정](https://azure.microsoft.com/pricing/details/storage/) 페이지를 참조하세요.

Hello 액세스 계층을 변경 하는 저장소 계정, 청구할 수 Blob에 대 한 hello에 대 한 요금이 변경 또한 toochanging 가격 합니다. Hello를 참조 하십시오 [Blob 저장소 계정-가격 및 요금 청구](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) 내용을 확인 합니다.

### <a name="manage-your-storage-access-keys"></a>저장소 액세스 키 다시 관리
저장소 계정을 만들 때 Azure hello 저장소 계정에 액세스할 때 인증에 사용 되는 두 개의 512 비트 저장소 액세스 키를 생성 합니다. 두 개의 저장소 액세스 키를 제공 함으로써 Azure를 사용 하면 중단 tooyour 저장소 서비스와 액세스 toothat 서비스 없는 tooregenerate hello 키입니다.

> [!NOTE]
> 저장소 액세스 키를 다른 사람과 공유하지 않는 것이 좋습니다. 사용할 수 있습니다 toopermit toostorage 리소스 액세스 키를 정지 하지 않고도 액세스 한 *공유 액세스 서명을*합니다. 공유 액세스 서명을 지정 하는 hello 사용 권한 및 사용자가 정의한 간격에 대 한 계정에 대 한 액세스 tooa 리소스를 제공 합니다. 자세한 내용은 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md) 을 참조하세요.
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>저장소 액세스 키 보기 및 복사
Hello에 [Azure 포털](https://portal.azure.com), tooyour 저장소 계정을 탐색, 클릭 **모든 설정을** 클릭 하 고 **액세스 키** tooview, 복사 및 계정 액세스 키 다시 생성 합니다. hello **선택 키** 블레이드에 toouse 응용 프로그램에서 복사할 수 있음을 기본 및 보조 키를 사용 하 여 미리 구성 된 연결 문자열도 포함 됩니다.

#### <a name="regenerate-storage-access-keys"></a>저장소 액세스 키 다시 생성
Tooyour 저장소 계정을 정기적으로 저장소 연결 보안 toohelp 유지 hello 선택 키를 변경 하는 것이 좋습니다. 두 개의 액세스 키에는 다른 선택 키 hello를 다시 생성 하는 동안에 하나의 선택 키를 사용 하 여 연결 toohello 저장소 계정을 유지 관리할 수 있도록 할당 됩니다.

> [!WARNING]
> 액세스 키 다시 생성 하는 hello 저장소 계정에 의존 하는 응용 프로그램 뿐만 아니라 Azure에서 서비스 영향을 줄 수 있습니다. Hello 액세스 키 tooaccess hello 저장소 계정을 사용 하는 모든 클라이언트에 업데이트 된 toouse hello에 대 한 새 키 여야 합니다.
> 
> 

**미디어 서비스** -저장소 계정에 의존 하는 미디어 서비스를 사용 하도록 설정한 경우 다시 동기화 해야 hello 선택 키를 미디어 서비스 hello 키를 다시 생성 합니다.

**응용 프로그램** -웹 응용 프로그램 또는 클라우드 서비스를 사용 하 여 hello 저장소 계정 손실 됩니다 hello 연결 키를 다시 생성 하는 경우 키 롤 하지 않는 한 경우.

**저장소 탐색기** -를 사용 하는 경우 [저장소 탐색기 응용 프로그램](storage-explorers.md), 해당 응용 프로그램에서 사용 되는 tooupdate hello 저장소 키를 시켜야 합니다.

저장소 액세스 키를 회전 하기 위한 hello 프로세스는 다음과 같습니다.

1. Hello 저장소 계정의 프로그램 응용 프로그램 코드 tooreference hello 보조 액세스 키의 hello 연결 문자열을 업데이트 합니다.
2. 저장소 계정에 대 한 hello 기본 액세스 키 다시 생성 합니다. Hello에 **선택 키** 블레이드에서 클릭 **Key1 다시 생성**, 클릭 하 고 **예** tooconfirm toogenerate 새 키를 지정 하 합니다.
3. 코드 tooreference hello 새 기본 액세스 키의 hello 연결 문자열을 업데이트 합니다.
4. Regenerate hello 보조 액세스 키를 hello 동일한 방식으로 합니다.

## <a name="delete-a-storage-account"></a>저장소 계정 삭제
tooremove 더 이상 사용 하는 저장소 계정을 탐색 hello toohello 저장소 계정의 [Azure 포털](https://portal.azure.com)를 클릭 하 고 **삭제**합니다. 저장소 계정 삭제 hello 전체 계정, 모든 데이터를 포함 하 여 hello 계정에서 삭제 됩니다.

> [!WARNING]
> 불가능 toorestore 삭제 된 저장소 계정 또는 hello 콘텐츠를 삭제 하기 전에 목록에 포함 된 모든 검색 됩니다. Hello 계정을 삭제 하기 전에 toosave를 원하는 있는지 tooback 향상 됩니다. 이 모든 리소스에 대 한 true hello 계정에서-blob, 테이블, 큐 또는 파일을 삭제 하면 영구적으로 삭제 됩니다.
> 

Azure 가상 컴퓨터와 연결 된 저장소 계정을 toodelete 시도 하면 아직 사용 중인 hello 저장소 계정에 대 한 오류가 발생할 수 있습니다. 이 오류의 문제를 해결하는 도움말은 [저장소 계정을 삭제할 때 오류 문제 해결](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
* [Microsoft Azure 저장소 탐색기](../../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.
* [Azure Blob 저장소: 쿨 및 핫 계층](../blobs/storage-blob-storage-tiers.md)
* [Azure 저장소 복제](storage-redundancy.md)
* [Azure 저장소 연결 문자열 구성](../storage-configure-connection-string.md)
* [Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](storage-use-azcopy.md)
* Hello 방문 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)합니다.

