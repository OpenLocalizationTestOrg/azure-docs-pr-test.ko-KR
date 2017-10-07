---
title: "aaaIntroduction tooAzure 저장소 | Microsoft Docs"
description: "소개 tooAzure 저장소, hello 클라우드에서 Microsoft의 데이터를 저장 합니다."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Azure 저장소 소개 tooMicrosoft

Microsoft Azure Storage는 가용성, 보안, 내구성, 확장성 및 중복성이 높은 저장소를 제공하는 Microsoft 관리 클라우드 서비스입니다. Microsoft는 유지 관리를 담당하고 사용자에 대한 중요한 문제를 처리합니다. 

Azure Storage는 Blob Storage, File Storage 및 Queue Storage라는 세 개의 데이터 서비스로 구성됩니다. Blob 저장소는 프리미엄 저장소만 Ssd를 사용 하 여 가장 빠른 성능이 가능한 hello에 대 한 표준 및 프리미엄 저장소를 지원 합니다. 다른 기능은 toostorage 많은 양의 저렴 한 비용에 대 한 거의 액세스 하는 데이터를 허용 하는 쿨 저장소입니다.

이 문서에서는 다음 hello에 대 한 설명:
* hello Azure 저장소 서비스
* hello 종류의 저장소 계정
* Blob, 큐 및 파일에 액세스
* 암호화
* 복제 
* 저장소 간에 데이터 전송
* 사용할 수 있는 많은 저장소 클라이언트 라이브러리를 hello 합니다. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Hello Azure 저장소 서비스를 소개합니다.

먼저 toouse hello 서비스 정보가 제공-Blob 저장소, 파일 저장 및 큐 저장소-Azure 저장소에서 저장소 계정을 만들고 해당 저장소 계정에 특정 서비스의 데이터를 전송할 수 있습니다. 

## <a name="blob-storage"></a>Blob 저장소

Blob은 기본적으로 사용자가 컴퓨터(또는 태블릿, 모바일 장치 등)에 저장한 항목과 같은 파일입니다. 사진, Microsoft Excel 파일, HTML 파일, 가상 하드 디스크(VHD), 로그와 같은 빅 데이터, 데이터베이스 백업 등 거의 모든 것이 가능합니다. Blob은 유사한 toofolders 컨테이너에 저장 됩니다. 

Blob 저장소에 파일을 저장 한 후에 액세스할 수 있습니다 어디에서 나 Url을 사용 하는 hello world hello REST 인터페이스 또는 hello Azure SDK 저장소 클라이언트 라이브러리 중 하나입니다. 저장소 클라이언트 라이브러리는 Node.js, Java, PHP, Ruby, Python 및 .NET을 비롯한 여러 언어에서 사용할 수 있습니다. 

블록 Blob, 추가 Blob 및 페이지 Blob라는 세 가지 Blob 유형이 있습니다.

* 블록 blob는 tooabout 일반 파일을 사용 하는 toohold 4.7 TB입니다. 
* 페이지 blob는 크기가 too8 TB 사용 하는 toohold 임의 액세스 파일입니다. 이러한 Vm을 백업 하는 hello VHD 파일에 사용 됩니다.
* 추가 blob는 hello 블록 blob와 같은 블록으로 구성 된 하지만에 맞게 최적화 된 작업을 추가 합니다. 이러한 여러 Vm에서 동일한 blob 정보 toohello 로깅 등의 작업에 사용 됩니다.

매우 큰 데이터 집합을 업로드 하거나 비현실적 hello 유선을 통해 데이터 tooBlob 저장소 다운로드 네트워크 제약 조건을 확인 하는 위치, 하드 드라이브 tooMicrosoft tooimport 집합이 제공 하거나 hello 데이터 센터에서 직접 데이터를 내보낼 수 있습니다. 참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](../storage-import-export-service.md)합니다.

## <a name="file-storage"></a>File Storage

Azure 파일 서비스 hello hello 표준 서버 메시지 블록 (SMB) 프로토콜을 사용 하 여 액세스할 수 있는 항상 사용 가능한 네트워크 파일 공유를 tooset이 있습니다. 여러 Vm을 공유할 수 있다는 것을 의미 동일을 hello 읽기 및 쓰기 권한이 모두 있는 파일입니다. Hello REST 인터페이스 또는 hello 저장소 클라이언트 라이브러리를 사용 하 여 hello 파일을 읽을 수도 있습니다. 

Azure 파일 저장소에서 회사 파일 공유에 파일을 구별 하는 한 가지는 어디에서 든 hello 파일을 액세스할 수 있도록 toohello 파일을 가리키는 공유 액세스 서명 (SAS) 토큰을 포함 하는 URL을 사용 하는 hello world에 있습니다. SAS 토큰을 생성할 수 있습니다. 특정 기간에 대 한 특정 액세스 tooa 개인 자산을 허용합니다. 

파일 공유는 다음과 같은 여러 가지 일반적인 시나리오에 사용할 수 있습니다. 

* 여러 온-프레미스 응용 프로그램에서 파일 공유를 사용합니다. 이 기능을 통해 보다 쉽게 toomigrate 데이터 tooAzure를 공유 하는 해당 응용 프로그램입니다. 탑재할 hello에 같은 드라이브 문자 hello 하는 파일 공유 toohello 온-프레미스 응용 프로그램 사용 하 여, 있는 경우에 최소한 변경 하 여 hello 파일 공유에 액세스 하는 응용 프로그램의 hello 부분 작동 해야 합니다.

* 구성 파일을 파일 공유에 저장하고 여러 VM에서 액세스할 수 있습니다. 도구 및 유틸리티를 그룹에 여러 개발자가 사용 되는 모든 사용자에 게 찾을 수 있도록, 확인 하는 파일 공유에 저장할 수 있으며를 사용 하는 hello 동일한 버전입니다.

* 진단 로그, 메트릭 및 크래시 덤프는 세 개의 예 tooa 파일 공유를 작성 및 처리 하거나 나중에 분석할 수 있는 데이터입니다.

이 시간, Active Directory 기반 인증 및 액세스 제어 목록 (Acl) 지원 되지 않으며, 없지만 이후 hello에 수 있습니다. hello 저장소 계정 자격 증명이 사용 되는 tooprovide 인증 액세스 toohello 파일 공유에 대 한 합니다. 즉, 탑재 hello 공유와 모든 사용자가 모든 읽기/쓰기 액세스 toohello 공유 해야 합니다.

## <a name="queue-storage"></a>큐 저장소

hello Azure 큐 서비스 사용 되는 toostore 및 검색 하 고 메시지 수입니다. 큐 메시지의 크기 (kb) too64 될 수 있습니다 및 큐에는 수많은 메시지 포함 될 수 있습니다. 큐는 일반적으로 사용 되는 toostore 목록이 메시지 toobe 비동기적으로 처리 합니다. 

예를 들어 고객 toobe 수 tooupload 그림 및 각 사진에 대 한 toocreate 축소판 그림을 원하는 합니다. Hello 사진을 업로드 하는 동안 대기 하면 toocreate hello 미리 보기에 대 한 고객을 가질 수 있습니다. 대신 toouse 큐 것입니다. Hello 고객 그의 업로드를 완료 하는 경우 메시지 toohello 큐를 작성 합니다. 다음 기능이 Azure hello 큐에서 hello 메시지를 검색 하 고 hello 축소판 그림을 만듭니다. 이 처리 hello 부분의 각각을 확장할 수 있습니다 별도로 사용량에 대 한 튜닝 하는 경우 더 세밀 하 게 합니다.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>테이블 저장소
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
이제 표준 Azure Table Storage는 Cosmos DB의 일부입니다. 또한 처리량 최적화 테이블, 글로벌 분포 및 자동 보조 인덱스를 제공하는 Azure Table Storage에 대한 프리미엄 테이블이 제공됩니다. 더 많은 toolearn을 시작 하 고 hello 새로운 premium 환경에서는 아웃 하십시오 체크 아웃 [Azure Cosmos DB: 테이블 API](https://aka.ms/premiumtables)합니다.

## <a name="disk-storage"></a>디스크 저장소

또한 hello Azure 저장소 팀 디스크, 가상 컴퓨터에서 사용 하는 모든 관리 되는 hello 포함 되어 기능과 관리 되지 않는 디스크를 소유 합니다. 이러한 기능에 대 한 자세한 내용은 hello를 참조 하십시오 [계산 서비스 설명서](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)합니다.

## <a name="types-of-storage-accounts"></a>저장소 계정 유형 

이 표에 hello 다양 한 종류의 저장소 계정 및 개체를 사용할 수 있습니다.

|**저장소 계정의 유형**|**범용 표준**|**범용 프리미엄**|**Blob Storage, 핫 및 쿨 액세스 계층**|
|-----|-----|-----|-----|
|**지원되는 서비스**| Blob, File, Queue 서비스 | Blob Service | Blob Service|
|**지원되는 Blob 유형**|블록 Blob, 페이지 Blob 및 추가 Blob | 페이지 Blob | 블록 Blob 및 추가 Blob|

### <a name="general-purpose-storage-accounts"></a>범용 저장소 계정

범용 저장소 계정에는 두 가지가 있습니다. 

#### <a name="standard-storage"></a>Standard Storage 

hello 가장 널리 사용 되는 저장소 계정 되는 모든 유형의 데이터에 사용할 수 있는 표준 저장소 계정이 있습니다. 표준 저장소 계정은 자기 미디어 toostore 데이터를 사용합니다.

#### <a name="premium-storage"></a>Premium Storage

프리미엄 저장소는 VHD 파일에 주로 사용되는 페이지 Blob에 고성능 저장소를 제공합니다. 프리미엄 저장소 계정 SSD toostore 데이터를 사용합니다. 모든 VM에 Premium Storage를 사용하는 것이 좋습니다.

### <a name="blob-storage-accounts"></a>Blob Storage 계정

hello Blob 저장소 계정은 특수 저장소 계정 toostore 블록 blob을 사용 하 고 추가 blob입니다. 이러한 계정에 페이지 Blob을 저장할 수 없습니다. 따라서 VHD 파일을 저장할 수 없습니다. 액세스 계층 tooHot tooset 또는 쿨;이 계정을 사용 하면 hello 계층은 언제 든 지 변경할 수 있습니다. 

자주 액세스 하는 파일에 대 한 hello 핫 액세스 계층은 사용 하는 등의 저장소에 대 한 비용이 많이 드는 비용을 지불 되지만 hello blob에 액세스 하는 hello 비용이 훨씬 낮습니다. Hello 쿨 액세스 계층에 저장 된 blob에 대 한 hello blob 액세스를 위한 비용이 많이 드는 비용을 지불 있지만 hello 저장소 비용을 훨씬 낮습니다.

## <a name="accessing-your-blobs-files-and-queues"></a>Blob, 파일 및 큐에 액세스

각 저장소 계정에는 모든 작업에 사용할 수 있는 두 개의 인증 키가 있습니다. Hello 롤오버할 수 있도록 두 개의 키 tooenhance 보안 키 가끔 있습니다. hello 계정 이름과 함께 소유 하는 hello 저장소 계정에서 tooall 데이터에 무제한 액세스를 허용 하기 때문에 이러한 키 수 안전 하 게 보호 합니다. 

이 섹션은 두 가지 방법으로 toosecure hello 저장소 계정 및 해당 데이터를 찾습니다. 저장소 계정 및 사용자 데이터를 보호 하는 방법에 대 한 자세한 내용은 참조 hello [Azure 저장소 보안 가이드](storage-security-guide.md)합니다.

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Azure AD를 사용 하 여 toostorage 계정을 액세스 보안

한 가지 방법은 toosecure 액세스 tooyour 저장소 데이터 액세스 toohello 저장소 계정 키를 제어 하 여는입니다. 리소스 관리자 역할 기반 액세스 제어 (RBAC) 사용 하 여 역할 toousers, 그룹 또는 응용 프로그램을 할당할 수 있습니다. 이러한 역할에 연결 된 tooa 특정 집합이 허용 되거나 허용 되지 않는 작업입니다. Toogrant 액세스 tooa 저장소 계정 RBAC를 사용 하 여 hello 액세스 계층을 변경 하는 등 해당 저장소 계정에 대 한 hello 관리 작업을 처리만 합니다. 특정 컨테이너 또는 파일 공유와 같은 RBAC toogrant 액세스 toodata 개체를 사용할 수 없습니다. 그러나 RBAC toogrant 액세스 toohello 저장소 계정 키를 사용 하는 tooread hello 데이터 개체 수를 사용할 수 있습니다. 

### <a name="securing-access-using-shared-access-signatures"></a>공유 액세스 서명을 사용하여 액세스 보호 

액세스 정책 toosecure 데이터 개체를 저장 한 공유 액세스 서명을 사용할 수 있습니다. 공유 액세스 서명 (SAS) 일 수 있는 보안 토큰을 포함 하는 문자열 toohello URI toodelegate toospecific 저장소 개체 액세스 및 사용 권한 및 액세스의 hello 날짜/시간 범위와 같은 toospecify 제약 조건 수 있는 자산에 대 한 연결입니다. 이 기능에는 광범위한 기능이 있습니다. 자세한 내용은 참조 너무[공유 액세스 서명 (SAS)를 사용 하 여](storage-dotnet-shared-access-signature-part-1.md)합니다.

### <a name="public-access-tooblobs"></a>공용 액세스 tooblobs

Blob 서비스 hello tooprovide 공용 액세스 tooa 컨테이너와 해당 blob 또는 blob에 특정 있습니다. 컨테이너 또는 Blob을 공개로 지정하면 모든 사용자가 이 컨테이너 또는 Blob를 익명으로 읽을 수 있으며 인증이 필요 없습니다. Toodo 하려는 경우의 예 이미지, 비디오 또는 Blob 저장소의 문서를 사용 하는 웹 사이트가 있는 경우 이것이입니다. 자세한 내용은 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>암호화

Hello 저장소 서비스에 사용할 수 있는 기본적인 종류의 암호화의 두 가지가 있습니다. 

### <a name="encryption-at-rest"></a>휴지 상태의 암호화 

Azure 저장소 계정의 Blob 서비스 hello 하거나 hello 파일 서비스 (미리 보기) 중 하나에 저장소 서비스 암호화 SSE ()를 설정할 수 있습니다. Toohello 특정 서비스를 작성 하는 모든 데이터는 암호화를 사용 하는 경우 기록 되기 전에 합니다. 암호가 해독 된 hello 데이터를 읽을 때 반환 전에 합니다. 

### <a name="client-side-encryption"></a>클라이언트 쪽 암호화

hello 저장소 클라이언트 라이브러리는 메서드를 호출할 수 tooprogrammatically hello 클라이언트 tooAzure에서 hello 네트워크를 통해 보내기 전에 데이터를 암호화 합니다. 암호화되어 저장됩니다. 즉, 휴지 시 암호화됩니다. 다시 hello 데이터를 읽을 때 받은 이후 hello 정보를 해독 합니다. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>전송 시 Azure 파일 공유에서 암호화

공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](../storage-dotnet-shared-access-signature-part-1.md)을 참조하세요. 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](../blobs/storage-manage-access-to-resources.md) 및 [hello Azure 저장소 서비스에 대 한 인증](https://msdn.microsoft.com/library/azure/dd179428.aspx) 보안 액세스 tooyour 저장소 계정에 대 한 자세한 내용은 합니다.

저장소 계정 및 암호화 보안에 대 한 자세한 내용은 참조 hello [Azure 저장소 보안 가이드](storage-security-guide.md)합니다.

## <a name="replication"></a>복제

데이터가 지속 됩니다 순서 tooensure, Azure 저장소에 hello 기능 tookeep (있고 관리) 데이터의 여러 복사본입니다. 이를 복제 또는 중복성이라고 합니다. 저장소 계정을 설정할 때 복제 형식을 선택합니다. 대부분의 경우에서 hello 저장소 계정이 설정 되 면이 설정을 수정할 수 있습니다. 

모든 저장소 계정에는 **LRS(로컬 중복 저장소)**가 있습니다. Hello 데이터 센터에서 Azure 저장소에서 관리 되는 데이터의 세 개의 복사본이 즉 hello 저장소 계정을 설정 되었으므로 설정할 때 지정 합니다. 때 변경 내용이 커밋된 tooone 복사을 hello 다른 두 개의 복사본이 업데이트 됩니다 성공을 반환 하기 전에. 즉, hello 세 개의 복제본은 항상 동기화 합니다. 또한 hello 세 복사본이 별도 오류 도메인에 있는 및 업그레이드 도메인, 즉, 데이터를 보유 하는 저장소 노드 실패 하거나 오프 라인 toobe 수행한 업데이트 되는 경우에 데이터를 사용할 수 있습니다. 

**LRS(로컬 중복 저장소)**

위에서 설명한 대로 LRS에서 세 개의 데이터 복사본이 단일 데이터 센터에 있습니다. 저장소 노드 실패 또는 오프 라인 toobe 업데이트를 수행 하지만 사용할 수 없게 되는 전체 데이터 센터의 대/소문자를 하지 hello 사용 하지 못하게 될 데이터의 hello 문제를 처리 합니다.

**ZRS(영역 중복 저장소)**

영역 중복 저장소 (ZRS) 데이터의 세 가지 로컬 복사본 hello 뿐만 아니라 다른 3 개 데이터 집합 유지 관리합니다. hello 세 복사본이의 두 번째 집합은 비동기적으로 복제 하나 또는 두 개의 영역 내에서 데이터 센터입니다. ZRS는 범용 저장소 계정에서 블록 Blob에만 사용할 수 있습니다. 또한 저장소 계정을 만든 하 고 ZRS를 선택한 후 변환할 수는 없습니다 것 toouse tooany 다른 복제의 경우, 또는 그 반대로 입력 합니다.

ZRS 계정은 LRS보다 높은 지속성을 제공하지만 메트릭 또는 로깅 기능은 제공하지 않습니다. 

**GRS(지역 중복 저장소)**

지역 중복 저장소 (GRS)에 기본 지역에서 데이터의 세 가지 로컬 복사본 hello 및 다른 3 개 보조 지역 수백 킬로미터 떨어진 hello 기본 지역에서에서 데이터 집합 유지 관리합니다. Hello 기본 지역에서 작업이 실패의 hello 이벤트에서 Azure 저장소는 toohello 보조 지역의 실패 합니다. 

**RA-GRS(읽기 액세스 지역 중복 저장소)** 

읽기 액세스 지역 중복 저장소는 GRS 똑같이 같지만 hello 보조 위치에 대 한 읽기 액세스 toohello 데이터를 얻게 점에서 차이가 있습니다. 기본 데이터 센터 hello 일시적으로 사용할 수 없게 되 tooread hello 데이터 hello 보조 위치에서 계속할 수 있습니다. 이는 매우 유용할 수 있습니다. 예를 들어 업데이트를 사용할 수 없는 경우에 일부 액세스할 수 있도록 웹 응용 프로그램을 읽기 전용 모드로 변경 하 고 toohello 보조 복사본이 있을 수 있습니다. 

> [!IMPORTANT]
> 어떻게 데이터가 복제 되어 저장소 계정의 만든 후 hello 계정을 만들 때 ZRS를 지정 하지 않으면 변경할 수 있습니다. 그러나는 추가 일회성 데이터 전송 LRS tooGRS 또는 RA-GRS에서 전환 비용을 청구할 수 있습니다 note 합니다.
>

복제에 대한 자세한 내용은 [Azure Storage 복제](storage-redundancy.md)를 참조하세요.

재해 복구 정보를 참조 하십시오. [Azure 저장소 중단이 발생할 경우 어떤 toodo](storage-disaster-recovery-guidance.md)합니다.

방법의 예에 대 한 RA-GRS 저장소 tooensure 높은 가용성, tooleverage 참조 [항상 사용 가능한 응용 프로그램 설계 RA-GRS를 사용 하 여](storage-designing-ha-apps-with-ragrs.md)합니다.

## <a name="transferring-data-tooand-from-azure-storage"></a>Azure 저장소에서 데이터 tooand 전송

저장소 계정 내에서 또는 저장소 계정에서 hello AzCopy 명령줄 유틸리티 toocopy blob 및 파일 데이터를 사용할 수 있습니다. 에 대 한 도움말 문서 hello 다음 중 하나를 참조 하십시오.

* [Windows에서 AzCopy를 사용하여 데이터 전송](storage-use-azcopy.md)
* [Linux에서 AzCopy를 사용하여 데이터 전송](storage-use-azcopy-linux.md)

AzCopy hello 위에 빌드됩니다. 따라서 [Azure 데이터 이동을 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), 미리 보기에서 현재 사용할 수 있습니다.

hello Azure 가져오기/내보내기 서비스에 사용 되는 tooimport 또는 내보내기 많은 양의 저장소 계정에서 blob 데이터 tooor 될 수 있습니다. Hello 데이터 hello 하드 드라이브에서 여러 하드 드라이브 tooan Azure 데이터 센터에서는 전송 여기서 메일 및 hello 하드 드라이브 다시 tooyou 보낼 준비 합니다. Hello 가져오기/내보내기 서비스에 대 한 자세한 내용은 참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](../storage-import-export-service.md)합니다.

## <a name="pricing"></a>가격

Azure 저장소에 대 한 가격에 대 한 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/storage/blobs/)합니다.

## <a name="storage-apis-libraries-and-tools"></a>Storage API, 라이브러리 및 도구
Azure Storage 리소스는 HTTP/HTTPS 요청을 수행할 수 있는 모든 언어로 액세스할 수 있습니다. 또한 Azure storage는 많이 사용되는 몇 가지 언어를 위한 프로그래밍 라이브러리를 제공합니다. 이 라이브러리는 동기/비동기 호출, 작업 일괄 처리, 예외 관리, 자동 재시도, 작업자 동작 등과 같은 세부 사항을 처리하여 Azure Storage 작업의 많은 측면을 간소화합니다. 다음 언어 hello에 대 한 현재 사용할 수 있는지 확인 하 고 플랫폼에서 다른 사용자와 hello 파이프라인:

### <a name="azure-storage-data-services"></a>Azure Storage 데이터 서비스
* [저장소 서비스 REST API](/rest/api/storageservices/)
* [.NET용 저장소 클라이언트 라이브러리](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Java/Android용 저장소 클라이언트 라이브러리](https://azure.microsoft.com/develop/java/)
* [Node.js용 저장소 클라이언트 라이브러리](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [PHP용 저장소 클라이언트 라이브러리](https://azure.microsoft.com/develop/php/)
* [Python용 저장소 클라이언트 라이브러리](https://azure.microsoft.com/develop/python/)
* [Ruby용 저장소 클라이언트 라이브러리](https://azure.microsoft.com/develop/ruby/)
* [PowerShell용 Storage Cmdlet](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [CLI 2.0의 저장소 명령](/cli/azure/storage)

## <a name="next-steps"></a>다음 단계

* [Blob Storage에 대한 세부 정보](../blobs/storage-blobs-introduction.md)
* [File Storage에 대한 세부 정보](../storage-files-introduction.md)
* [Queue Storage에 대한 세부 정보](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>관리자용
* [Azure Storage와 함께 Azure PowerShell 사용](storage-powershell-guide-full.md)
* [Azure Storage에서 Azure CLI 사용](../storage-azure-cli.md)

### <a name="for-net-developers"></a>.NET 개발자용
* [.NET을 사용하여 Azure Blob 저장소 시작](../blobs/storage-dotnet-how-to-use-blobs.md)
* [.NET을 사용하여 Azure 테이블 저장소 시작](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [.NET을 사용하여 Azure 큐 저장소 시작](../storage-dotnet-how-to-use-queues.md)
* [Windows에서 Azure 파일 저장소 시작](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Java/Android 개발자용
* [어떻게 toouse Java에서 Blob 저장소](../blobs/storage-java-how-to-use-blob-storage.md)
* [어떻게 toouse Java에서 테이블 저장소](../../cosmos-db/table-storage-how-to-use-java.md)
* [어떻게 toouse Java에서 큐 저장소](../storage-java-how-to-use-queue-storage.md)
* [어떻게 toouse Java에서 파일 저장소](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Node.js 개발자용
* [어떻게 toouse Node.js에서 Blob 저장소](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [어떻게 toouse Node.js에서 테이블 저장소](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [어떻게 toouse Node.js에서 큐 저장소](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>PHP 개발자용
* [어떻게 toouse PHP에서 Blob 저장소](../blobs/storage-php-how-to-use-blobs.md)
* [어떻게 toouse PHP에서 테이블 저장소](../../cosmos-db/table-storage-how-to-use-php.md)
* [어떻게 toouse PHP에서 큐 저장소](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Ruby 개발자용
* [어떻게 toouse Ruby에서 Blob 저장소](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [어떻게 toouse Ruby에서 테이블 저장소](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [어떻게 toouse Ruby에서 큐 저장소](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Python 개발자용
* [어떻게 toouse Python에서 Blob 저장소](../blobs/storage-python-how-to-use-blob-storage.md)
* [어떻게 toouse Python에서 테이블 저장소](../../cosmos-db/table-storage-how-to-use-python.md)
* [어떻게 toouse Python에서 큐 저장소](../storage-python-how-to-use-queue-storage.md)   
* [어떻게 toouse Python에서 파일 저장소](../storage-python-how-to-use-file-storage.md) 
-->