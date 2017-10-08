---
title: "aaaHow toocreate 관리 또는 hello Azure 클래식 포털에서에서 저장소 계정을 삭제 | Microsoft Docs"
description: "새 저장소 계정 만들기, 계정 액세스 키를 관리 또는 hello Azure 포털에서에서 저장소 계정을 삭제 합니다. 표준 및 프리미엄 저장소 계정에 대해 알아봅니다."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 5e4f4360-3f81-4d63-a0b1-e7771b67af11
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 6ee2359e02c7c9e9c111e1fc87a6160bb8b785b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Azure 저장소 계정 정보
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-try-azure-tools](../../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>개요
Azure 저장소 계정에서는 toohello Azure Blob, 큐, 테이블 및 파일 서비스를 Azure 저장소에 액세스할 수는 있습니다. 저장소 계정에 대 한 Azure 저장소에 데이터 개체가 hello 고유한 네임 스페이스를 제공합니다. Hello 계정의 데이터는 기본적으로 사용할 수 있는 유일한 tooyou hello 계정 소유자입니다.

저장소 계정에는 다음과 같은 두 종류가 있습니다.

* 표준 저장소 계정에는 Blob, 테이블, 큐 및 파일 저장소가 포함됩니다.
* 프리미엄 저장소 계정은 현재 Azure 가상 컴퓨터 디스크만 지원합니다. 프리미엄 저장소의 자세한 개요는 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](storage-premium-storage.md) 를 참조하세요.

## <a name="storage-account-billing"></a>저장소 계정 사용 비용
Azure 저장소 사용 비용은 저장소 계정에 따라 청구됩니다. 저장소 비용은 저장소 용량, 복제 체계, 저장소 트랜잭션 및 데이터 송신의 네 가지 요소를 기반으로 합니다.

* 저장소 용량 참조 toohow 훨씬 저장소 계정 서비스 toostore 데이터를 사용 하는 합니다. 데이터의 양을으로 저장 하는 이며 어떻게 복제는 단순히 데이터를 저장 hello 비용을 결정 합니다.
* 복제에 따라 한 번에 유지 관리되는 데이터의 복사본 수 및 위치가 결정됩니다.
* 트랜잭션을은 tooall 읽기를 작업 tooAzure 저장소 쓰기 나타냅니다.
* 데이터 유출은 toodata Azure 영역 외부로 전송 합니다. 저장소 계정의 hello 데이터 액세스 응용 프로그램에서 실행 하지 않는 hello 같은 지역의 여부는 응용 프로그램은 클라우드 서비스 또는 다른 유형의 응용 프로그램을 다음 데이터 유출 요금이 청구 됩니다. (Azure 서비스에 대해 수행할 수 데이터와 서비스 단계 toogroup hello에 동일한 데이터 센터 tooreduce 또는 데이터 전송 요금을 제거 합니다.)  

hello [Azure 저장소 가격](https://azure.microsoft.com/pricing/details/storage) 스토리지 용량, 복제 및 트랜잭션에 대 한 가격 책정 세부 정보를 제공 합니다. hello [데이터 전송 가격 정보](https://azure.microsoft.com/pricing/details/data-transfers/) 데이터 유출 가격 책정 세부 정보를 제공 합니다.

저장소 계정 용량 및 성능 목표에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)를 참조하세요.

> [!NOTE]
> Azure 가상 컴퓨터를 만들 때 저장소 계정 수에 대 한 경우 자동으로 만들어집니다 hello 배포 위치에서 해당 위치에 저장소 계정을 아직 없는 있습니다. 따라서 가상 컴퓨터 디스크에 대 한 저장소 계정 toocreate 아래 필요한 toofollow hello 단계는 없습니다. hello 저장소 계정 이름은 hello 가상 컴퓨터 이름 기반 이어야 합니다. Hello 참조 [Azure 가상 컴퓨터 설명서](https://azure.microsoft.com/documentation/services/virtual-machines/) 내용을 확인 합니다.
> 
> 

## <a name="create-a-storage-account"></a>저장소 계정 만들기
1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. 클릭 **새로** hello hello 페이지 맨 아래에 hello 작업 표시줄에서 합니다. **Data Services** | **저장소**를 선택한 다음 **빨리 만들기**를 클릭합니다.
   
    ![NewStorageAccount](./media/storage-create-storage-account-classic-portal/storage_NewStorageAccount.png)
3. **URL**에 저장소 계정의 이름을 입력합니다.
   
   > [!NOTE]
   > 저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다.
   > 
   > 저장소 계정 이름은 Azure 내에서 고유해야 합니다. Azure 클래식 포털 hello 선택한 hello 저장소 계정 이름은 이미 사용 하는 경우 표시 됩니다.
   > 
   > 
   
    참조 [저장소 계정 끝점](#storage-account-endpoints) 아래에 대 한 세부 정보 hello 저장소 계정 이름을 사용 하는 tooaddress 되는 방식을 하는 방법에 대 한 Azure 저장소의 개체입니다.
4. **위치/선호도 그룹**, 닫기 tooyou 또는 tooyour 고객은 저장소 계정의 위치를 선택 합니다. 저장소 계정에는 데이터가 Azure 가상 컴퓨터 또는 클라우드 서비스 등 다른 Azure 서비스에서 액세스 되는 경우 tooselect hello 목록 toogroup에서 선호도 그룹 hello에서 저장소 계정의 다른 Azure 서비스와 동일한 데이터 센터 사용 하 고 있는지 tooimprove 성능 및 비용을 절감 합니다.
   
    저장소 계정을 만들 때 선호도 그룹을 선택해야 합니다. 기존 계정 tooan 선호도 그룹을 이동할 수 없습니다. 선호도 그룹에 대한 자세한 내용은 아래의 [선호도 그룹과 서비스 공동 배치](#service-co-location-with-an-affinity-group) 를 참조하세요.
   
   > [!IMPORTANT]
   > 구독에 사용할 수 있는 위치는 toodetermine, hello를 호출할 수 있습니다 [모든 리소스 공급자 나열](https://msdn.microsoft.com/library/azure/dn790524.aspx) 작업 합니다. PowerShell에서 toolist 공급자 호출 [Get AzureLocation](https://msdn.microsoft.com/library/azure/dn757693.aspx)합니다. .NET에서 hello를 사용 하 여 [목록](https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.provideroperationsextensions.list.aspx) hello ProviderOperationsExtensions 클래스의 메서드.
   > 
   > 또한 어떤 지역에서 어떤 서비스가 가능한지에 대한 자세한 정보는 [Azure 지역](https://azure.microsoft.com/regions/#services) 을 참조하세요.
   > 
   > 
5. Azure 구독이 여러 개 있는 경우 다음 hello **구독** 필드가 표시 됩니다. **구독**, hello toouse hello 저장소 계정에 사용할 Azure 구독을 입력 합니다.
6. **복제**, 선택 hello 원하는 수준의 저장소 계정에 대 한 복제 합니다. hello 복제 옵션은 데이터에 대 한 내 구성을 최대화를 제공 하는 지리적 중복 복제 하는 것이 좋습니다. Azure 저장소 복제 옵션에 대한 자세한 내용은 아래의 [Azure 저장소 복제](storage-redundancy.md)를 참조하세요.
7. **저장소 계정 만들기**를 클릭합니다.
   
    몇 분 toocreate 저장소 계정의 걸릴 수 있습니다. toocheck hello 상태 hello hello Azure 클래식 포털 맨 아래에 hello 알림을 모니터링할 수 있습니다. 새 저장소 계정에 hello 저장소 계정이 생성 된 후 **온라인** 상태 이며 사용 하기 위해 준비 합니다.

![StoragePage](./media/storage-create-storage-account-classic-portal/Storage_StoragePage.png)

### <a name="storage-account-endpoints"></a>저장소 계정 끝점
Azure 저장소에 저장되는 모든 개체에는 고유한 URL 주소가 있습니다. hello 저장소 계정 이름 형식은 hello 해당 주소의 하위 도메인입니다. hello는 특정 tooeach 서비스 하위 도메인 및 도메인 이름 조합이 형성 된 *끝점* 저장소 계정에 대 한 합니다.

예를 들어 저장소 계정의 이름이 *mystorageaccount*, 저장소 계정에 대 한 hello 기본 끝점은 다음:

* Blob 서비스: http://*mystorageaccount*.blob.core.windows.net
* Table service: http://*mystorageaccount*.table.core.windows.net
* 큐 서비스: http://*mystorageaccount*.queue.core.windows.net
* 파일 서비스: http://*mystorageaccount*.file.core.windows.net

Hello hello 저장소 대시보드에서 저장소 계정에 대 한 hello 끝점을 볼 수 있습니다 [Azure 클래식 포털](https://manage.windowsazure.com) 면 hello 계정이 생성 되었습니다.

저장소 계정에는 개체에 액세스 하기 위한 hello URL hello 저장소 계정 toohello 끝점에서 hello 개체의 위치를 추가 하 여 만들어집니다. 예를 들어 Blob 주소의 형식은 다음과 같습니다. http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*

사용자 지정 도메인 이름을 toouse 스토리지 계정으로 구성할 수도 있습니다. 자세한 내용은 [Blob 저장소 끝점에 대한 사용자 지정 도메인 이름 구성](storage-custom-domain-name.md) 을 참조하세요.

### <a name="service-co-location-with-an-affinity-group"></a>선호도 그룹과 서비스 공동 배치
*선호도 그룹* 은 Azure 저장소 계정을 사용하여 Azure 서비스와 VM을 지리적으로 그룹화한 것을 말합니다. 선호도 그룹에 동일한 데이터 센터 또는 대상 사용자 그룹 hello 근처 hello 컴퓨터 작업량을 두어 서비스 성능을 향상 시킬 수 있습니다. 또한 청구 요금이 청구 되지 발생 수신을 위해 hello의 일부인 다른 서비스에서 저장소 계정 데이터에에서 액세스할 때 동일한 선호도 그룹.

> [!NOTE]
> toocreate 선호도 그룹을 열고 hello <b>설정</b> hello의 영역 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 <b>선호도 그룹</b>, 다음 중 하나를 클릭 하 고 <b>추가 프로그램 선호도 그룹</b> 또는 hello <b>추가</b> 단추입니다. 만들고 및 hello Azure 서비스 관리 API를 사용 하 여 선호도 그룹을 관리할 수도 있습니다. 자세한 내용은 <a href="http://msdn.microsoft.com/library/azure/ee460798.aspx">선호도 그룹 작업</a>을 참조하세요.
> 
> 

## <a name="view-copy-and-regenerate-storage-access-keys"></a>저장소 액세스 키 보기, 복사 및 다시 생성을 참조하세요.
저장소 계정을 만들 때 Azure hello 저장소 계정에 액세스할 때 인증에 사용 되는 두 개의 512 비트 저장소 액세스 키를 생성 합니다. 두 개의 저장소 액세스 키를 제공 함으로써 Azure를 사용 하면 중단 tooyour 저장소 서비스와 액세스 toothat 서비스 없는 tooregenerate hello 키입니다.

> [!NOTE]
> 저장소 액세스 키를 다른 사람과 공유하지 않는 것이 좋습니다. 사용할 수 있습니다 toopermit toostorage 리소스 액세스 키를 정지 하지 않고도 액세스 한 *공유 액세스 서명을*합니다. 공유 액세스 서명을 지정 하는 hello 사용 권한 및 사용자가 정의한 간격에 대 한 계정에 대 한 액세스 tooa 리소스를 제공 합니다. 자세한 내용은 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md) 을 참조하세요.
> 
> 

Hello에 [Azure 클래식 포털](https://manage.windowsazure.com)를 사용 하 여 **키 관리** hello 대시보드 또는 hello **저장소** tooview/복사 / 재생성 hello 저장소 액세스 키 사용 되는 페이지 tooaccess hello Blob, 테이블 및 큐 서비스입니다.

### <a name="copy-a-storage-access-key"></a>저장소 액세스 키 복사
사용할 수 있습니다 **키 관리** toocopy 저장소 액세스 키 toouse 연결 문자열에 있습니다. hello 연결 문자열 hello 저장소 계정 이름 및 인증에서 키 toouse 필요합니다. 연결을 구성 하는 방법에 대 한 정보는 Azure 저장소 서비스 tooaccess 문자열, 참조 [Azure 저장소 연결 문자열 구성](storage-configure-connection-string.md)합니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **저장소**, hello 저장소 계정 tooopen hello 대시보드의 hello 이름을 클릭 하 고 있습니다.
2. **키 관리**를 클릭합니다.
   
     **액세스 키 관리** 가 열립니다.
   
    ![키 관리](./media/storage-create-storage-account-classic-portal/Storage_ManageKeys.png)
3. toocopy 저장소 액세스 키를 선택 하는 hello 키 텍스트입니다. 그런 다음 마우스 오른쪽 단추를 클릭하고 **복사**를 클릭합니다.

### <a name="regenerate-storage-access-keys"></a>저장소 액세스 키 다시 생성
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
2. 저장소 계정에 대 한 hello 기본 액세스 키 다시 생성 합니다. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 보낸 사람 hello 대시보드 또는 hello **구성** 페이지 **키 관리**합니다. 클릭 **다시 생성** 아래에서 기본 액세스 키를 hello 하 고 클릭 한 다음 **예** tooconfirm 원하는 toogenerate 새 키입니다.
3. 코드 tooreference hello 새 기본 액세스 키의 hello 연결 문자열을 업데이트 합니다.
4. Hello 보조 액세스 키 다시 생성 합니다.

## <a name="delete-a-storage-account"></a>저장소 계정 삭제
사용 하 여 저장소 계정 더 이상 사용 하는 tooremove **삭제** hello 대시보드 또는 hello **구성** 페이지. **삭제** 삭제 hello hello 계정에서 모든 hello blob, 테이블 및 큐를 포함 하 여 전체 저장소 계정입니다.

> [!WARNING]
> 불가능 toorestore 삭제 된 저장소 계정 또는 hello 콘텐츠를 삭제 하기 전에 목록에 포함 된 모든 검색 됩니다. Hello 계정을 삭제 하기 전에 toosave를 원하는 있는지 tooback 향상 됩니다. 이 모든 리소스에 대 한 true hello 계정에서-blob, 테이블, 큐 또는 파일을 삭제 하면 영구적으로 삭제 됩니다.
> 
> 저장소 계정에는 Azure 가상 컴퓨터에 대 한 VHD 파일이 있으면 다음 삭제 해야 이미지와 hello 저장소 계정을 삭제 하려면 먼저 해당 VHD 파일을 사용 하는 디스크. 먼저, 실행 되 고 삭제 하는 경우에 hello 가상 컴퓨터를 중지 합니다. toodelete 디스크 이동 toohello **디스크** 탭 하 고 있는 모든 디스크를 삭제 합니다. toodelete 이미지 이동 toohello **이미지** 탭 및 hello 계정에 저장 되어 있는 모든 이미지를 삭제 합니다.
> 
> 

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com), 클릭 **저장소**합니다.
2. Hello 이름 제외 하 고 hello 저장소 계정 항목에서 아무 곳 이나 클릭 한 다음 클릭 **삭제**합니다.
   
     -또는-
   
    Hello 저장소 계정 tooopen hello 대시보드의의 hello 이름을 클릭 한 다음 클릭 **삭제**합니다.
3. 클릭 **예** tooconfirm toodelete hello 저장소 계정이 되도록 합니다.

## <a name="next-steps"></a>다음 단계
* Azure 저장소에 대해 자세히 toolearn 참조 hello [Azure 저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)합니다.
* Hello 방문 [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)합니다.
* [Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](storage-use-azcopy.md)

