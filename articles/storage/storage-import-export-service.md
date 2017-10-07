---
title: "blob 저장소에서 Azure 가져오기/내보내기 tootransfer 데이터 tooand aaaUsing | Microsoft Docs"
description: "Toocreate 가져오고 내보내기 hello 데이터 tooand blob 저장소에서 전송 하기 위해 Azure 포털에서에서 작업에 알아봅니다."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 84471d736d2433ffee9f49fbef91856d3dd56bb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>Hello Microsoft Azure 가져오기/내보내기 서비스 tootransfer 데이터 tooblob 저장소를 사용 하 여
Azure 가져오기/내보내기 서비스 hello toosecurely 전송 많은 양의 데이터 tooAzure blob 저장소가 배송 하드 디스크 드라이브 tooan Azure 데이터 센터에서 있습니다. Azure blob 저장소 toohard 디스크 드라이브에서이 서비스 tootransfer 데이터를 사용 하 고 tooyour 온-프레미스 사이트를 제공할 수도 있습니다. 이 서비스는 경우에 적합 한 tootransfer 데이터 tooor azure에서의 몇 가지 tb (테라바이트)를 원하는 되지만 경우가 업로드 또는 다운로드 hello 네트워크를 통해 toolimited 대역폭 인해 부적합 하거나 높은 네트워크 비용입니다.

hello 서비스에서는 하드 디스크 드라이브는 BitLocker 데이터의 보안 hello에 대 한 암호화를 수 있어야 합니다. hello 서비스 지원 두 hello 클래식 및 Azure 리소스 관리자 저장소 계정 (표준 및 쿨 계층) 공용 Azure의 hello 영역 모두에 존재 합니다. 이 문서의 뒷부분에 지정 된 지원 hello 위치의 tooone 하드 디스크 드라이브를 배송 해야 합니다.

이 문서에서는 자세한 있습니다 hello Azure 가져오기/내보내기 서비스 및 Azure Blob 저장소에서 데이터 tooand 복사 하기 위한 tooship 드라이브 하는 방법에 대 한.

## <a name="when-should-i-use-hello-azure-importexport-service"></a>Hello Azure 가져오기/내보내기 서비스는 때 사용 해야 합니까?
업로드 하거나 네트워크 속도가 너무 느린 hello를 통해 데이터를 다운로드 하거나 추가 네트워크 대역폭을 가져오는 것은 비용 때 Azure 가져오기/내보내기 서비스를 사용 하는 것이 좋습니다.

다음과 같은 시나리오에서 이 서비스를 사용할 수 있습니다.

* 마이그레이션 데이터 toohello 클라우드: 비용 효과적인 및 많은 양의 데이터 tooAzure 신속 하 게 이동 합니다.
* 콘텐츠 배포: 신속 하 게 데이터 tooyour 고객 사이트를 전송 합니다.
* 온-프레미스 데이터 toostore의 백업을 Azure blob 저장소에서 수행 하는 백업: 합니다.
* 데이터 복구: 많은 양의 blob 저장소에 저장 된 데이터를 복구 하 고 전달할 tooyour 온-프레미스 위치입니다.

## <a name="prerequisites"></a>필수 조건
이 섹션에 나열 hello 필수 구성 요소에 대 한 필수 toouse이이 서비스 합니다. 드라이브를 발송하기 전에 주의 깊게 검토하세요.

### <a name="storage-account"></a>저장소 계정
기존 Azure 구독 및 하나 이상의 저장소 계정 toouse hello 가져오기/내보내기 서비스 있어야 합니다. 각 작업에는 하나의 저장소 계정에서 사용 되는 tootransfer 데이터 tooor 될 수 있습니다. 다시 말해, 하나의 가져오기/내보내기 작업이 여러 저장소 계정에서 사용될 수 없습니다. 새 저장소 계정을 만드는 방법에 대 한 정보를 참조 하십시오. [어떻게 tooCreate 저장소 계정](storage-create-storage-account.md#create-a-storage-account)합니다.

### <a name="blob-types"></a>Blob 형식
Azure 가져오기/내보내기 서비스 toocopy 데이터도 사용할 수 있습니다**블록** blob 또는 **페이지** blob입니다. 반대로 이 서비스를 사용하여 Azure 저장소에서 **블록** Blob, **페이지** Blob 또는 **추가** Blob을 내보내기만 할 수도 있습니다.

### <a name="job"></a>작업
toobegin hello를 가져오는 프로세스의 Blob 저장소에서 내보내기 tooor, 먼저 작업을 만듭니다. 작업은 가져오기 작업 또는 내보내기 작업이 될 수 있습니다.

* Azure 저장소 계정에 온-프레미스 tooblobs 제공 tootransfer 데이터 가져오기 작업을 만듭니다.
* 내보내기 작업 만들기 hello 가져오기/내보내기 서비스를 발송할 것임 하나 또는 둘 하드 드라이브 tooan Azure 알림 tootransfer 현재 저장 된 데이터를 blob을 저장소 계정 toohard 드라이브 있는 작업을 만들 때 tooyou.s 제공 하려는 경우 데이터 센터입니다.

* 가져오기 작업의 경우 데이터가 포함된 하드 드라이브가 발송됩니다.
* 내보내기 작업의 경우 빈 하드 드라이브가 발송됩니다.
* 작업당 too10 하드 디스크 드라이브를 제공할 수 있습니다.

Import를 만들려는 하거나 hello Azure 포털 또는 hello를 사용 하 여 작업을 내보낼 수 있습니다 [Azure 저장소 가져오기/내보내기 REST API](/rest/api/storageimportexport)합니다.

### <a name="waimportexport-tool"></a>WAImportExport 도구
hello 만드는 첫 번째 단계는 **가져올** 작업 tooprepare 가져오기에 대 한 제공 될 프로그램 드라이브만 있으면 됩니다. tooprepare 드라이브, tooa 로컬 서버와 실행된 hello WAImportExport 도구 hello 로컬 서버에 연결 해야 합니다. 이 WAImportExport 도구 데이터 toohello 드라이브에 복사, hello BitLocker 드라이브에 hello 데이터를 암호화 및 hello 드라이브 저널 파일 생성을 용이 하 게 합니다.

hello 저널 파일 작업 및 저장소 계정 이름 및 드라이브 일련 번호와 같은 드라이브에 대 한 기본 정보를 저장합니다. 이 저널 파일 hello 드라이브에 저장 되지 않습니다. 가져오기 작업을 만드는 동안 사용됩니다. 이 문서의 뒷부분에는 작업을 만들기 위한 단계별 세부 내용이 제공됩니다.

hello WAImportExport 도구 에서만 64 비트 Windows 운영 체제와 호환 됩니다. Hello 참조 [운영 체제](#operating-system) 지원 되는 특정 운영 체제 버전에 대 한 섹션.

최신 버전의 hello hello 다운로드 [WAImportExport 도구](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip)합니다. 사용에 대 한 자세한 내용은 hello WAImportExport 도구, 참조 hello [WAImportExport 도구를 사용 하 여 hello](storage-import-export-tool-how-to.md)합니다.

>[!NOTE]
>**이전 버전:** 할 수 있습니다 [WAImportExpot V1 다운로드](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) 버전의 hello 도구를 너무 참조[WAImportExpot V1 사용 가이드](storage-import-export-tool-how-to-v1.md)합니다. WAImportExpot V1 버전의 hello 도구에 대 한 지원을 제공지 않습니다 **데이터는 이미 미리 작성 된 toohello 디스크 때 디스크를 준비**합니다. 또한 hello만 키를 사용할 수는 SAS 키 경우 toouse WAImportExpot V1 도구에 필요 합니다.

>

### <a name="hard-disk-drives"></a>하드 디스크 드라이브
SSD 또는 2.5"또는 3.5 인치 SATA II 또는 III 내부 HDD만 2.5 인치 가져오기/내보내기 서비스 hello로 사용 하기 위해 지원 됩니다. 단일 가져오기/내보내기 작업에는 최대 10개의 HDD/SSD가 있을 수 있으며, 개별 HDD/SSD는 임의 크기일 수 있습니다. 많은 수 드라이브의 여러 작업에 분산 되 고 hello 만들 수 있는 작업 수에 제한이 없는 있습니다. 

가져오기 작업에 대 한만 hello 첫 번째 데이터 볼륨 hello 드라이브에 처리 됩니다. hello 데이터 볼륨은 NTFS로 포맷 되어야 합니다.

> [!IMPORTANT]
> 기본 제공 USB 어댑터와 함께 제공되는 외부 하드 디스크 드라이브는 이 서비스에서 지원하지 않습니다. 또한 외부 HDD의 hello 대/소문자 내 hello 디스크를 사용할 수 없습니다. 외부 Hdd를 전송 하지 마십시오.
> 
> 

Toocopy 데이터 toointernal Hdd를 사용 하는 외부 USB 어댑터의 목록을 다음과 같습니다. Anker 68UPSATAA-02BU Anker 68UPSHHDS-BU Startech SATADOCK22UE Orico 6628SUS3-C-BK(6628 Series) Thermaltake BlacX 핫스왑 SATA 외부 하드 드라이브 도킹 스테이션(USB 2.0 및 eSATA)

### <a name="encryption"></a>암호화
hello 데이터 hello 드라이브에서 BitLocker 드라이브 암호화를 사용 하 여 암호화 되어야 합니다. 이렇게 하면 전송 중 데이터가 보호됩니다.

가져오기 작업에 대 한 두 가지 방법으로 tooperform hello 암호화가 있습니다. 드라이브 준비 하는 동안 hello WAImportExport 도구를 실행 하는 동안 데이터 집합 CSV 파일을 사용 하는 경우 첫 번째 방법은 hello는 toospecify hello 옵션입니다. 두 번째 방법은 hello는 hello 드라이브에 수동으로 tooenable BitLocker 암호화 하 고 드라이브 준비 하는 동안 WAImportExport 도구 명령줄을 실행 하는 경우 hello driveset CSV의에서 hello 암호화 키를 지정 합니다.

내보내기 작업에 대 한 데이터가 복사 toohello 드라이브 형식이 되 면 hello 서비스 암호화 백 tooyou 출시 하기 전에 BitLocker를 사용 하 여 hello 드라이브. 암호화 키 hello tooyou hello Azure 포털을 통해 제공 됩니다.  

### <a name="operating-system"></a>운영 체제
Hello 64 비트 운영 체제 tooprepare hello 하드 드라이브 hello WAImportExport 도구를 사용 하 여 hello 드라이브 tooAzure 출시 하기 전에 다음 중 하나를 사용할 수 있습니다.

Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Pro, Windows 8 Enterprise, Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. 이러한 모든 운영 체제는 BitLocker 드라이브 암호화를 지원합니다.

### <a name="locations"></a>위치
hello Azure 가져오기/내보내기 서비스는 모든 공용 Azure 저장소 계정에서 데이터 tooand 복사를 지원합니다. 다음 위치 hello tooone 하드 디스크 드라이브를 제공할 수 있습니다. 저장소 계정을 만들 때 대체 배송 위치 제공 될 여기에서 지정 되지 않은 공용 Azure 위치에 있으면는 hello Azure 포털 사용 하 여 hello 작업 또는 가져오기/내보내기 REST API를 환영 합니다.

지원되는 발송 위치:

* 미국 동부
* 미국 서부
* 미국 동부 2
* 미국 서부 2
* 미국 중부
* 미국 중북부
* 미국 중남부
* 미국 중서부
* 북유럽
* 서유럽
* 동아시아
* 동남아시아
* 오스트레일리아 동부
* 오스트레일리아 남동부
* 일본 서부
* 일본 동부
* 인도 중부
* 인도 남부
* 인도 서부
* 캐나다 중부
* 캐나다 동부
* 브라질 남부
* 한국 중부
* 미국 정부 버지니아
* 미국 정부 아이오와
* 미국 국방부 동부
* 미국 국방부 중부
* 중국 동부
* 중국 북부
* 영국 남부

### <a name="shipping"></a>발송
**배송 드라이브 toohello 데이터 센터:**

가져오기 또는 내보내기 작업을 만들 때 제공 됩니다 hello 중 하나의 배송 주소 위치 tooship 드라이브를 지원 합니다. hello 배달 주소 제공 된 저장소 계정의 hello 위치에 따라 달라 집니다 하지만 저장소 계정 위치와 같은 hello 아닐 수 있습니다.

주소를 전달 하 여 드라이브 toohello FedEx, DHL, UPS 또는 hello 미국 우편 서비스 tooship 같은 운송 업체를 사용할 수 있습니다.

**Hello 데이터 센터에서 드라이브를 배송:**

가져오기 또는 내보내기 작업을 만들 때 배송 hello 드라이브 백업 작업이 완료 되는 경우 Microsoft toouse에 대 한 반환 주소를 제공 해야 합니다. 처리 지연 tooavoid 유효한 반환 주소를 입력 했는지 확인 하십시오.

사용자가 선택한 이동 통신 사업자 순서 tooforward ship hello 하드 디스크에서 사용할 수 있습니다. hello carrier 순서 toomaintain 체인의 적절 한 추적을 해야 합니다. 도 제공 해야 올바른 FedEx 또는 DHL 운송 업체 계정 번호 toobe hello 드라이브 다시 배송에 대 한 Microsoft에서 사용 합니다. FedEx 계정 번호는 hello 미국 및 유럽 위치에서 다시 드라이브 배송에 필요 합니다. 아시아 및 오스트레일리아 위치에서 드라이브를 다시 배송하려면 DHL 계정 번호가 필요합니다. 계정 번호가 없을 경우 [FedEx](http://www.fedex.com/us/oadr/)(미국 및 유럽) 또는 [DHL](http://www.dhl.com/)(아시아 및 오스트레일리아) 운송업체 계정을 만들 수 있습니다. 운송업체 계정 번호가 이미 있는 경우 이 계정 번호가 유효한지 확인하세요.

패키지를 제공 하는 경우에 hello 조건을 따라야 [Microsoft Azure 서비스 약관](https://azure.microsoft.com/support/legal/services-terms/)합니다.

> [!IMPORTANT]
> 전달 hello 실제 미디어 toocross 국경을 할 수 note 하십시오. 실제 미디어 및 데이터는 가져올 및/또는 되는지 hello 관련 법률에 따라 내보낸 것을 확인 합니다. 하기 전에 hello 실제 미디어 제공 되는 경우 확인 즉 관리자 tooverify 미디어 및 데이터 식별 된 배송된 toohello 데이터 센터 수 합법적으로 있습니다. 이 경우에 Microsoft 적절 한 시기에 도달 tooensure를 도움이 됩니다. 예를 들어, 국경을 교차 하는 모든 패키지 (경우에 유럽 연합 안의 테두리를 교차) 제외 hello 패키지와 함께 제공 하는 상업용 송장 toobe가 필요 합니다. Hello 상업용 송장 통신 회사 웹 사이트에서의 채워진된 복사본을 인쇄할 수 있습니다. 상업 송장의 예로 [DHL 상업 송장](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf)과 [FedEx 상업 송장](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf)이 있습니다. Microsoft는 hello 내보내기와 표시 되지 있는지 확인 합니다.
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>Hello Azure 가져오기/내보내기 서비스는 어떻게 작동 합니까?
온-프레미스 사이트와 hello Azure 가져오기/내보내기 서비스를 사용 하 여 작업을 만들고 하드 디스크 드라이브 tooan Azure 데이터 센터를 전달 하 여 Azure blob 저장소 간에 데이터를 전송할 수 있습니다. 발송하는 각 하드 디스크 드라이브는 단일 작업과 연결됩니다. 각 작업은 단일 저장소 계정과 연결됩니다. 검토 hello [필수 구성 요소 섹션](#pre-requisites) 이 서비스와 같은 지원 blob 유형, 디스크 유형, 위치 및 배송의 hello 세부 사항에 대 한 toolearn 신중 하 게 합니다.

이 섹션에서는 가져오기 관련 된 높은 수준의 hello 단계에 설명 하 고 내보내기 작업 합니다. Hello의 뒷부분에 나오는 [빠른 시작 섹션](#quick-start), 작업 내보내기 및 가져오기 toocreate 단계별 지침을 제공 합니다.

### <a name="inside-an-import-job"></a>가져오기 작업 내부
상위 수준에서 가져오기 작업에 단계를 수행 하는 hello 포함 됩니다.

* Hello 해야 하는 드라이브의 수 및 가져온 hello 데이터 toobe를 결정 합니다.
* Blob 저장소의 데이터에에서 대 한 hello 대상 blob 위치를 식별 합니다.
* 사용 하 여 더 많은 하드 디스크 드라이브 또는 데이터 tooone WAImportExport 도구 toocopy hello 및 BitLocker로 암호화 합니다.
* Hello Azure 포털을 사용 하 여 대상 저장소 계정에 가져오기 작업 만들기 또는 가져오기/내보내기 REST API hello 합니다. Hello Azure 포털을 사용 하는 경우 hello 드라이브 저널 파일을 업로드 합니다.
* Hello 반환 주소 및 hello 드라이브 백 tooyou 전달에 사용 되는 운송 업체 계정 번호 toobe 제공 합니다.
* 배송 hello 하드 디스크 드라이브 toohello 작업 만들기 중에 제공 된 주소를 전달 합니다.
* Hello 배달 추적 hello 가져오기 작업 정보에 번호를 업데이트 하 고 hello 가져오기 작업을 제출 합니다.
* 드라이브를 받아 hello Azure 데이터 센터에서 처리 됩니다.
* 드라이브는 캐리어 계정 toohello 반송 주소 hello 가져오기 작업에 제공 된를 사용 하 여 제공 됩니다.
  
    ![그림 1: 가져오기 작업 흐름](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>내보내기 작업 내부
상위 수준에서 내보내기 작업에 단계를 수행 하는 hello 포함 됩니다.

* Hello 데이터 toobe.msi 파일로 내보내고 hello 해야 하는 드라이브의 수를 결정 합니다.
* Hello 원본 blob 또는 컨테이너의 Blob 저장소의 데이터에에서는 경로 식별 합니다.
* Hello Azure 포털을 사용 하 여 원본 저장소 계정에서 내보내기 작업 만들기 또는 가져오기/내보내기 REST API hello 합니다.
* 원본 blob hello 또는 내보내기 작업의 hello 데이터 컨테이너 경로 지정 합니다.
* Toobe hello 드라이브 백 tooyou 전달에 사용 되는 hello 반환 주소 및 운송 업체 계정 번호를 제공 합니다.
* 배송 hello 하드 디스크 드라이브 toohello 작업 만들기 중에 제공 된 주소를 전달 합니다.
* Hello 배달 추적 hello 내보내기 작업 정보에 번호를 업데이트 하 고 hello 내보내기 작업을 제출 합니다.
* hello 드라이브를 받아 hello Azure 데이터 센터에서 처리 됩니다.
* hello 드라이브; BitLocker로 암호화 hello 키는 hello Azure 포털을 통해 사용할 수 있습니다.  
* hello 드라이브 캐리어 계정 toohello 반송 주소 hello 가져오기 작업에 제공 된를 사용 하 여 제공 됩니다.
  
    ![그림 2: 내보내기 작업 흐름](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>작업 및 드라이브 상태 보기
가져오기의 hello 상태를 추적 하거나 hello Azure 포털에서에서 작업을 내보낼 수 있습니다. Hello 클릭 **가져오기/내보내기** 탭 합니다. 작업 목록 hello 페이지에 표시 됩니다.

![작업 상태 보기](./media/storage-import-export-service/jobstate.png)

Hello hello 프로세스에서 사용자의 드라이브 위치에 따라 작업 상태를 다음 중 하나가 표시 됩니다.

| 작업 상태 | 설명 |
|:--- |:--- |
| 만드는 중 | 작업을 만든 후 해당 상태가 tooCreating 설정 됩니다. Hello 작업 만들기 상태 hello 상태인 동안 hello 가져오기/내보내기 서비스에서는 hello 드라이브를 배송된 toohello 데이터 센터 않았습니다. 작업은 tootwo 주, 지나면 hello 서비스에 의해 삭제 자동으로 구성에 대 한 hello 만들기 상태로 유지 될 수 있습니다. |
| 발송 | 패키지를 배송 한 후 hello 추적 hello Azure 포털에에서 대 한 정보를 업데이트 해야 합니다.  이를 "배송" hello 작업으로 바뀝니다. hello 작업 tootwo 주를 hello 배송 상태에 대 한 유지 됩니다. 
| 수신됨 | Hello 데이터 센터에 모든 드라이브를 받은 다음 받은 toohello hello 작업 상태가 설정 됩니다. |
| 전송 중 | 처리를 시작 하는 하나 이상의 드라이브 되 면 hello 작업 상태를 설정할 toohello 전송 합니다. Hello 드라이브 상태를 참조 하십시오. 자세한 내용은 아래 섹션. |
| 패키징 | 모든 드라이브 처리를 완료 한 후 hello 작업 hello 드라이브는 배송된 백 tooyou 될 때까지 hello 패키징 상태에 배치 됩니다. |
| Completed | 모든 드라이브 배송된 백 toohello 고객 된 hello 작업이 오류 없이 완료 된 경우, 다음 hello 작업 설정 됩니다 toohello 완료 됨 상태입니다. hello 작업 완료 됨 상태로 hello에서 90 일이 지나면 자동으로 삭제 됩니다. |
| 닫힘 | 모든 드라이브 배송된 백 toohello 고객 된 내용이 있는 경우 모든 오류 hello 작업의 hello 처리 하는 동안, 후 다음 hello 작업 설정 됩니다 toohello 닫힌된 상태입니다. hello Closed 상태에서 90 일이 지나면 hello 작업을 자동으로 삭제 될 됩니다. |

hello 표에서으로 가져오기 또는 내보내기 작업 전환 될 때 개별 드라이브의 hello 수명 주기를 설명 합니다. 작업의 각 드라이브의 현재 상태 hello hello Azure 포털에서에서 표시 됩니다.
hello 다음 표에서 각 상태는 작업의 각 드라이브를 통해 전달할 수 있습니다.

| 드라이브 상태 | 설명 |
|:--- |:--- |
| 지정됨 | 가져오기 작업에 대 한 hello Azure 포털에서에서 hello 작업이 만들어질 때 드라이브에 대 한 hello 초기 상태는 hello에 표시 된 상태입니다. 내보내기 작업에 대 한 hello 작업이 만들어질 때 드라이브를 지정 하므로 hello 초기 드라이브 상태는 hello Received 상태입니다. |
| 수신됨 | hello 드라이브 hello 가져오기/내보내기 서비스 운영자가 가져오기 작업에 대 한 회사를 전달 하는 hello 로부터 받은 hello 드라이브를 처리 하는 경우 toohello 받은 상태로 전환 됩니다. 내보내기 작업에 대 한 hello 초기 드라이브 상태는 hello Received 상태입니다. |
| 수신되지 않음 | hello 드라이브 hello 직업 패키지가 도착 했지만 hello 패키지 hello 드라이브를 포함 하지 않는 경우 toohello NeverReceived 상태를 이동 합니다. Hello 서비스 hello 배송 정보를 받았지만 hello 패키지 hello 데이터 센터에 아직 도착 하지 않은 후 2 주 후 경과 된 경우에이 상태로 드라이브를 이동할 수도 있습니다. |
| 전송 중 | 드라이브는 hello 서비스 tootransfer 데이터 hello 드라이브 tooWindows Azure 저장소에서에서 시작 될 때 toohello 전송 상태를 이동 합니다. |
| Completed | Hello 서비스 모든 hello 데이터를 오류 없이 성공적으로 전송 하는 경우 toohello 완료 됨 상태로 이동 됩니다.
| 완료됨(추가 정보 필요) | Toohello hello 서비스에서 문제가 발생 했습니다 일부 데이터를 복사 하는 동안에서 경우 CompletedMoreInfo 상태 또는 toohello 드라이브 이동 됩니다. hello 정보는 오류, 경고 또는 blob 덮어쓰기에 대 한 정보 메시지에 포함할 수 있습니다.
| 반송됨 | hello 데이터 센터 백 toohello 반송 주소에서 배송 되 면 hello 드라이브 toohello ShippedBack 상태를 이동 합니다. |

Hello Azure 포털의에서이 이미지를이 예제에서는 작업의 hello 드라이브 상태를 표시합니다.

![드라이브 상태 보기](./media/storage-import-export-service/drivestate.png)

hello 다음 표에 hello 드라이브 오류 상태와 각 상태에 대해 수행 하는 hello 작업이 있습니다.

| 드라이브 상태 | 이벤트 | 해결 방법/다음 단계 |
|:--- |:--- |:--- |
| 수신되지 않음 | 다른 배송으로 도착 (hello 작업 배송의 일부로 수신 되지 않았으므로) 이므로 NeverReceived 것으로 표시 되는 드라이브입니다. | hello 운영 팀 hello 드라이브 toohello Received 상태가 이동 합니다. |
| 해당 없음 | 작업의 일부가 아닌 드라이브는 다른 작업의 일부로 hello 데이터 센터에 도착 합니다. | hello 드라이브는 추가 드라이브로 표시 하 고 hello 원래 패키지와 관련 된 hello 작업이 완료 될 때 toohello 고객 반환 됩니다. |

### <a name="time-tooprocess-job"></a>시간 tooprocess 작업
hello tooprocess 배달 시간, 작업 유형 등의 다른 요인에 따라 달라 집니다 가져오기/내보내기 작업에 걸리는 시간은 입력 양과 hello 데이터를 복사 하 고 제공 된 hello 디스크의 크기를 hello의 크기입니다. hello 가져오기/내보내기 서비스는 SLA가 없습니다 하 하지만 hello 서비스 too10의 7 일 동안 toocomplete hello 복사를 노력 hello 디스크 받은 후 합니다. Hello REST API tootrack hello 작업 진행 상황을 더욱 긴밀 하 게 사용할 수 있습니다. Hello 선도 표시 복사 진행 작업 나열 작업에에서 백분율 전체 매개 변수 없는 경우 연락 toous 예상 toocomplete 시간이 중요 한 가져오기/내보내기 작업 해야 할 경우.

### <a name="pricing"></a>가격
**드라이브 취급 수수료**

가져오기 또는 내보내기 작업의 일부로 처리되는 각 드라이브에 대해 드라이브 취급 수수료가 있습니다. Hello에 hello 정보를 참조 하십시오. [Azure 가져오기/내보내기 가격](https://azure.microsoft.com/pricing/details/storage-import-export/)합니다.

**발송 비용**

TooAzure 드라이브를 배송 하는 경우에 hello 비용 toohello 운송 업체를 전달 해야 합니다. Microsoft hello 드라이브 tooyou 돌아오면 선적 비용 hello hello 작업 생성 시에 입력 한 toohello 운송 업체 계정을 청구 됩니다.

**트랜잭션 비용**

Blob 저장소로 데이터를 가져올 때는 트랜잭션 비용이 없습니다. blob 저장소에서 데이터를 내보낼 때 표준 전송 요금 hello 적용 됩니다. 트랜잭션 비용에 대한 자세한 내용은 [데이터 전송 가격 책정](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>빠른 시작
이 섹션에서 가져오기 및 내보내기 작업을 만드는 단계별 지침을 제공합니다. 모든 hello를 충족 하는지 확인 하십시오 [필수](#pre-requisites) 앞으로 이동 하기 전에.

> [!IMPORTANT]
> hello 서비스 가져오기 당 한 개의 표준 저장소 계정만 지원 또는 작업 내보내고 프리미엄 저장소 계정을 지원 하지 않습니다. 
> 
> 
## <a name="create-an-import-job"></a>가져오기 작업 만들기
데이터 toohello 지정 된 데이터 센터를 포함 하는 하나 이상의 드라이브를 배송 하드 드라이브에서 가져오기 작업 toocopy 데이터 tooyour Azure 저장소 계정 만들기 hello 가져오기 작업 전달 하드 디스크 드라이브에 대 한 세부 정보, 데이터 toobe 복사 대상 저장소 계정 및 toohello Azure 가져오기/내보내기 서비스 정보를 전달 합니다. 가져오기 작업 만들기는 3단계 프로세스입니다. 첫째, hello WAImportExport 도구를 사용 하 여 드라이브를 준비 합니다. 둘째, hello Azure 포털을 사용 하 여 가져오기 작업을 제출 합니다. 셋째, hello 드라이브 toohello 배달 작업 생성 및 업데이트 hello 작업 정보에 발송 정보 중에 제공 된 주소를 제공 합니다.   

### <a name="prepare-your-drives"></a>드라이브 준비
hello WAImportExport 도구를 사용해 서 드라이브 tooprepare는 hello Azure 가져오기/내보내기 서비스를 사용 하 여 데이터를 가져올 때 첫 번째 단계를 hello 합니다. 드라이브 tooprepare 아래 hello 단계를 수행 합니다.

1. 가져온 hello 데이터 toobe를 식별 합니다. 디렉터리 및 hello 로컬 서버에 독립 실행형 파일 또는 네트워크 공유 수 있습니다.  
2. Hello hello 데이터의 전체 크기에 따라 해야 하는 드라이브 수를 결정 합니다. Hello 필요한 수의 2.5 인치 SSD 또는 2.5"또는 3.5 인치 SATA II 또는 III 하드 디스크 드라이브를 확보 합니다.
3. Hello 대상 저장소 계정, 컨테이너, 가상 디렉터리 및 blob을 식별 합니다.
4.  Hello 디렉터리 및/또는 복사 된 tooeach 하드 디스크 드라이브 수 있는 독립 실행형 파일을 확인 합니다.
5.  Hello 데이터 집합 및 driveset CSV 파일을 만듭니다.
    
    **데이터 집합 CSV 파일**
    
    다음은 샘플 데이터 집합 CSV 파일의 예제입니다.
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    위 예제는 hello, 100M_1.csv.txt "containername" 라는 hello 컨테이너의 복사 toohello 루트 됩니다. Containername"hello 컨테이너 이름"가 없는 경우 만들어집니다. 모든 파일 및 50M_original 아래에 폴더를 재귀적으로 복사 toocontainername 됩니다. 폴더 구조는 유지됩니다.

    에 대 한 자세한 내용은 [hello dataset CSV 파일을 준비](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file)합니다.
    
    **기억**: 기본적으로 hello 데이터 블록 Blob으로 합니다. 페이지 Blob으로 hello BlobType 필드 값 tooimport 데이터를 사용할 수 있습니다. 예를 들어 Azure VM에 디스크로 탑재되는 VHD 파일을 가져오는 경우 페이지 Blob으로 가져와야 합니다.

    **드라이브 집합 CSV 파일**

    플래그는 hello 목록은 디스크 toowhich hello 드라이브 문자를 포함 하는 CSV 파일 도구 toocorrectly hello에 대 한 순서에 매핑된 hello driveset hello 값 hello의 선택 목록 디스크 toobe 준비 합니다. 

    다음은 driveset CSV 파일의 hello 예가입니다.
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    위 예제는 hello, 두 개의 디스크가 연결 되어 및 볼륨 문자 G:\ H:\와 기본 NTFS 볼륨을 만든 가정 합니다. hello 도구 포맷 하 고 H:\ 호스트 및 됩니다 하지 포맷 하거나 G:\ 볼륨 호스팅 hello 디스크를 암호화 하는 hello 디스크를 암호화 합니다.

    에 대 한 자세한 내용은 [hello driveset CSV 파일을 준비](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file)합니다.

6.  사용 하 여 hello [WAImportExport 도구](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) toocopy 데이터 tooone 또는 더 많은 하드 드라이브입니다.
7.  Hello 하드 디스크 드라이브에 drivset tooenable BitLocker 암호화를 CSV에 암호화 필드 "암호화"를 지정할 수 있습니다. 또는 수도 수동으로 hello 하드 디스크 드라이브에서 BitLocker 암호화를 설정 및 "AlreadyEncrypted"를 지정 하 고 hello 도구를 실행 하는 동안 hello driveset CSV의에서 hello 키를 제공 합니다.

8. 디스크 준비를 완료 한 후 hello hello 하드 디스크 드라이브 또는 hello 저널 파일에는 데이터를 수정 하지 마십시오.

> [!IMPORTANT]
> 준비하는 각 하드 디스크 드라이브는 저널 파일이 됩니다. Hello Azure 포털을 사용 하 여 hello 가져오기 작업을 만들 때 해당 가져오기 작업의 일부는 hello 드라이브의 모든 hello 저널 파일을 업로드 해야 합니다. 저널 파일이 없는 드라이브는 처리되지 않습니다.
> 
>

다음은 hello 명령 및 hello 하드 디스크 드라이브를 준비 하는 것에 대 한 예제를 사용 하 여 WAImportExport 도구입니다.

Hello에 대 한 PrepImport 명령을 WAImportExport 도구는 먼저 세션 toocopy 디렉터리 및/또는 새 복사 세션을 사용 하 여 파일에 복사 합니다.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**가져오기 예제 1**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

순서 대로 너무**드라이브 더 추가할**, 하나 수 새 driveset 파일을 만들고 아래와 같이 hello 명령을 실행 합니다. 후속 복사 세션 toohello 다른 디스크 드라이브에 대 한 지정 된 것 보다 InitialDriveset.csv 파일에 새 driveset CSV 파일을 지정 하 고 "AdditionalDriveSet" 값 toohello 매개 변수로 제공 합니다. 사용 하 여 hello **동일한 저널 파일** 이름을 지정 하 고 제공 된 **새 세션 ID**합니다. hello AdditionalDriveset CSV 파일 형식이 InitialDriveSet 형식과 일치 합니다.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**가져오기 예제 2**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

순서 tooadd 추가 데이터 toohello에서 동일한 driveset 후속 복사 세션 toocopy 추가 파일/디렉터리에 대 한 WAImportExport 도구 PrepImport 명령을 호출할 수 있습니다: 후속 복사 세션 toohello 동일한 하드 디스크 드라이브에 지정 된에 대 한 InitialDriveset.csv 파일, hello 지정 **동일한 저널 파일** 이름을 지정 하 고 제공는 **새 세션 ID**; 필요 tooprovide hello 저장소 계정 키가 있습니다.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**가져오기 예제 3**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

hello WAImportExport 도구를 사용 하는 방법에 대 한 자세한 내용을 보려면 [가져오기를 위한 하드 드라이브를 준비](storage-import-export-tool-preparing-hard-drives-import.md)합니다.

또한 toohello 참조 [워크플로 가져오기 작업을 위해 하드 드라이브 tooprepare 샘플](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) 자세한 단계별 지침.  

### <a name="create-hello-import-job"></a>Hello 가져오기 작업 만들기
1. 드라이브를 준비 했으면 hello Azure 포털에서에서 저장소 계정을 tooyour 찾아 hello 대시보드를 봅니다. **간략 상태**에서 **가져오기 작업 만들기**를 클릭합니다. Hello 단계를 검토 하 고 hello 확인란 tooindicate 드라이브를 준비한 및 hello 드라이브 저널 파일을 사용할 수 있는지를 선택 합니다.
2. 1 단계에서에서이 가져오기 작업 및 유효한 반송 주소에 대 한 hello 담당자의 연락처 정보를 제공 합니다. Hello 가져오기 작업에 대 한 자세한 정보 표시 로그 데이터 toosave 원한다 면 hello 옵션 선택 너무**내 'waimportexport' blob 컨테이너에서 hello 자세한 로그 저장**합니다.
3. 2 단계에서에서 hello 드라이브 준비 단계 중에 가져온 hello 드라이브 저널 파일을 업로드 합니다. 준비한 각 드라이브에 대해 tooupload 한 파일이 필요 합니다.
   
   ![가져오기 작업 만들기 - 3단계](./media/storage-import-export-service/import-job-03.png)
4. 3 단계에서에서 설명 하는 hello 가져오기 작업에 대 한 이름을 입력 합니다. Hello 이름에는 소문자, 숫자, 하이픈, 있을 수 있습니다 및 밑줄 문자로 시작 해야 하며 공백을 포함할 수 없습니다. Hello 이름을 선택 하면 tootrack 작업 진행 중에서이 고 완료 되 면 하는 동안 사용 합니다.
   
   다음을 hello 목록에서 데이터 센터 지역을 선택 합니다. hello 데이터 센터 지역 hello 데이터 센터와 패키지를 배송 해야 toowhich 주소를 표시 합니다. 자세한 내용은 아래 hello FAQ를 참조 하십시오.
5. 4 단계에서에서 반송 운송 업체 hello 목록에서 선택 하 고 운송 업체 계정 번호를 입력 합니다. 가져오기 작업이 완료 되 면 Microsoft는이 계정 tooship hello 드라이브 백 tooyou를 사용 합니다.
   
   추적 번호가 있으면 배달 운송 업체 hello 목록에서 선택한 추적 번호를 입력 합니다.
   
   추적 번호가 아직 선택 있는지 **패키지를 배송 한 후이 가져오기 작업에 대 한 내 배송 정보를 제공 합니다**, 다음 hello 가져오기 프로세스를 완료 합니다.
6. 패키지를 배송 한 후 추적 번호를 반환 tooenter toohello **가져오기/내보내기** hello Azure 포털에서에서 저장소 계정에 대 한 페이지 hello 목록에서 작업을 선택 하 고 선택 **발송 정보**. Hello 마법사를 통해 이동한 2 단계에서에서 추적 번호를 입력 합니다.
   
    추적 번호 hello hello 작업을 만드는 2 주 이내에 업데이트 되지 않으면, hello 작업이 만료 됩니다.
   
    Hello 작업 hello 만들기, 전달 또는 전송 상태에 있으면 hello 마법사의 2 단계에서에서 운송 업체 계정 번호를 업데이트할 수도 있습니다. Hello 작업 hello 패키징 상태가 되 면 해당 작업에 대 한 운송 업체 계정 번호를 업데이트할 수 없습니다.
7. Hello 포털 대시보드에서 작업 진행률을 추적할 수 있습니다. 참조 함으로써 의미 hello 이전 섹션에서 각 작업 상태 [작업 상태 보기](#viewing-your-job-status)합니다.

## <a name="create-an-export-job"></a>내보내기 작업 만들기
내보내기 작업 toonotify hello 발송 하나 또는 더 많은 빈 드라이브 toohello 데이터 센터 저장소 계정 toohello 드라이브에서 데이터를 내보낼 수 있으며, hello 드라이브 tooyou 제공 되도록 가져오기/내보내기 서비스를 만듭니다.

### <a name="prepare-your-drives"></a>드라이브 준비
내보내기 작업을 위한 드라이브 준비를 위해 다음 사전 검사를 수행하는 것이 좋습니다.

1. Hello hello WAImportExport 도구 PreviewExport 명령을 사용 하 여 필요한 디스크 수를 확인 합니다. 자세한 내용은 [내보내기 작업에 대한 드라이브 사용량 미리 보기](https://msdn.microsoft.com/library/azure/dn722414.aspx)를 참조하세요. 사용자가 선택한 hello blob의 드라이브 사용을 미리 볼 수, hello 드라이브의 hello 크기에 따라 보아야 toouse 합니다.
2. 있습니다 수 읽기/쓰기 hello 내보내기 작업에 대 한 제공 될 toohello 하드 드라이브를 확인 합니다.

### <a name="create-hello-export-job"></a>Hello 내보내기 작업 만들기
1. 내보내기 작업의 경우 toocreate hello Azure 포털에서에서 저장소 계정을 tooyour 찾아 hello 대시보드를 봅니다. 아래 **빠른 보기**, 클릭 **내보내기 작업 만들기** hello 마법사를 통해 계속 진행 합니다.
2. 2 단계에서에서이 내보내기 작업에 대 한 hello 담당자의 연락처 정보를 제공 합니다. Hello 내보내기 작업에 대 한 자세한 정보 표시 로그 데이터 toosave 원한다 면 hello 옵션 선택 너무**내 'waimportexport' blob 컨테이너에서 hello 자세한 로그 저장**합니다.
3. 3 단계에서에서 데이터를 tooexport 저장소 계정 tooyour 빈 값에서 드라이브 또는 드라이브는 blob를 지정 합니다. Hello 저장소 계정에서 모든 blob 데이터가 tooexport를 선택할 수 또는 blob 또는 blob tooexport의 집합을 지정할 수 있습니다.
   
   blob tooexport toospecify hello를 사용 하 여 **Equal To** 선택기 hello 컨테이너 이름으로 시작 hello 상대 경로 toohello blob를 지정 합니다. 사용 하 여 *$root* toospecify hello 루트 컨테이너입니다.
   
   모든 toospecify blob 접두사를 사용 하 여 hello로 시작 **으로 시작** 선택기에는 슬래시로 시작 하는 hello 접두사를 지정 하 고 '/'입니다. hello 접두사 hello 컨테이너 이름, hello 전체 컨테이너 이름 또는 hello 전체 컨테이너 이름 hello blob 이름의 hello 접두사 뒤의 hello 접두사 수 있습니다.
   
   다음 표에서 hello 유효한 blob 경로 예를 보여 줍니다.
   
   | 선택기 | Blob 경로 | 설명 |
   | --- | --- | --- |
   | 시작 단어 |/ |Hello 저장소 계정에서 모든 blob을 내보냅니다. |
   | 시작 단어 |/$root/ |Hello 루트 컨테이너의 모든 blob을 내보냅니다. |
   | 시작 단어 |/book |접두사 **book** |
   | 시작 단어 |/music/ |컨테이너 **music** |
   | 시작 단어 |/music/love |접두사 **love**로 시작하는 컨테이너 **music**의 모든 Blob을 내보냄 |
   | 너무 같음|$root/logo.bmp |내보내기 blob **logo.bmp** hello 루트 컨테이너에 |
   | 너무 같음|videos/story.mp4 |컨테이너 **videos**의 Blob **story.mp4**를 내보냄 |
   
   제공 해야 올바른 형식으로 hello blob 경로 tooavoid 오류 처리 하는 동안이 스크린 샷에 표시 된 것 처럼 합니다.
   
   ![내보내기 작업 만들기 - 3단계](./media/storage-import-export-service/export-job-03.png)
4. 4 단계에서에서 설명 하는 hello 내보내기 작업에 대 한 이름을 입력 합니다. 소문자, 숫자, 하이픈, hello 이름에 포함할 수 있으며 밑줄 문자로 시작 해야 하며 공백을 포함할 수 없습니다.
   
   hello 데이터 센터 지역 hello 데이터 센터 toowhich 패키지를 배송 해야 표시 됩니다. 자세한 내용은 아래 hello FAQ를 참조 하십시오.
5. 5 단계에서에서 hello 목록에서 반송 운송 업체를 선택 하 고 운송 업체 계정 번호를 입력 합니다. Microsoft는이 계정 tooship를 사용 하는 내보내기 작업이 완료 되 면 tooyou 드라이브에 백업 합니다.
   
   추적 번호가 있으면 배달 운송 업체 hello 목록에서 선택한 추적 번호를 입력 합니다.
   
   추적 번호가 아직 선택 있는지 **패키지를 배송 한 후이 내보내기 작업에 대 한 내 배송 정보를 제공 합니다**, 다음 hello 내보내기 프로세스를 완료 합니다.
6. 패키지를 배송 한 후 추적 번호를 반환 tooenter toohello **가져오기/내보내기** hello Azure 포털에서에서 저장소 계정에 대 한 페이지 hello 목록에서 작업을 선택 하 고 선택 **발송 정보**. Hello 마법사를 통해 이동한 2 단계에서에서 추적 번호를 입력 합니다.
   
    추적 번호 hello hello 작업을 만드는 2 주 이내에 업데이트 되지 않으면, hello 작업이 만료 됩니다.
   
    Hello 작업 hello 만들기, 전달 또는 전송 상태에 있으면 hello 마법사의 2 단계에서에서 운송 업체 계정 번호를 업데이트할 수도 있습니다. Hello 작업 hello 패키징 상태가 되 면 해당 작업에 대 한 운송 업체 계정 번호를 업데이트할 수 없습니다.
   
   > [!NOTE]
   > 내보낸 hello blob toobe hello 시점 toohard 드라이브 복사에 사용 중인 경우 Azure 가져오기/내보내기 서비스는 hello blob 및 스냅숏의 복사본 hello 스냅숏으로 걸립니다.
   > 
   > 
7. Hello Azure 포털의에서 hello 대시보드에 작업 진행률을 추적할 수 있습니다. 참조의 hello 이전 섹션에서 각 작업 상태 의미의 "사용자 작업 상태 보기"입니다.
8. Hello 드라이브 내보낸 데이터를 받은 후 볼 수 있으며 사용자의 드라이브에 대 한 hello 서비스에서 생성 한 hello BitLocker 키 복사. Hello Azure 포털에서에서 저장소 계정을 tooyour 이동한 hello 가져오기/내보내기 탭을 클릭 합니다. Hello 목록에서 내보내기 작업을 선택 하 고 hello 키 보기 단추를 클릭 합니다. hello BitLocker 키 아래와 같이 표시 됩니다.
   
   ![내보내기 작업의 BitLocker 키 보기](./media/storage-import-export-service/export-job-bitlocker-keys.png)

이 서비스를 사용 하는 경우 고객에 게 발생 하는 hello 가장 일반적인 질문을 포함 하는 대로 아래 hello FAQ 섹션을 통해 이동 하세요.

## <a name="frequently-asked-questions"></a>질문과 대답

**Hello Azure 가져오기/내보내기 서비스를 사용 하 여 Azure 파일 저장소를 복사할 수 있습니까?**

아니요, hello Azure 가져오기/내보내기 서비스 블록 Blob 및 페이지 Blob만 지원합니다. Azure File Storage, Table Storage 및 Queue Storage를 포함한 다른 모든 저장소 유형은 지원되지 않습니다.

**Hello Azure 가져오기/내보내기 서비스는 CSP 구독에 사용할 수 있습니까?**

Azure Import/Export 서비스는 CSP 구독을 지원합니다.

**가져오기 작업에 대 한 hello 드라이브 준비 단계 건너뛸 수 또는 복사 하지 않고도 드라이브를 준비할 수 있습니까?**

Hello Azure WAImportExport 도구를 사용 하 여 데이터를 가져오기 위한 tooship 하려는 모든 드라이브를 준비 해야 합니다. Hello WAImportExport 도구 toocopy 데이터 toohello 드라이브를 사용 해야 합니다.

**해야 tooperform 모든 디스크 준비 내보내기 작업을 만들 때?**

아니요, 하지만 일부 사전 검사를 수행하는 것이 좋습니다. Hello hello WAImportExport 도구 PreviewExport 명령을 사용 하 여 필요한 디스크 수를 확인 합니다. 자세한 내용은 [내보내기 작업에 대한 드라이브 사용량 미리 보기](https://msdn.microsoft.com/library/azure/dn722414.aspx)를 참조하세요. 사용자가 선택한 hello blob의 드라이브 사용을 미리 볼 수, hello 드라이브의 hello 크기에 따라 보아야 toouse 합니다. 또한 및 hello에 대 한 제공 될 쓰기 toohello 하드 드라이브에서 읽을 수 있는 확인 작업을 내보냅니다.

**요구 사항을 지원 실수로 toohello를 따르지 않는 경우는 HDD를 전송할 경우 어떻게 되나요?**

hello Azure 데이터 센터는 toohello 지원 요구 사항 tooyou를 따르지 않는 hello 드라이브를 반환 합니다. Hello 지원 요구 사항을 충족 일부 hello 드라이브 hello 패키지에만 해당 드라이브를 처리할지 및 hello 요구 사항을 충족 하지 않는 hello 드라이브 tooyou 반환 됩니다.

**작업을 취소할 수 있습니까?**

작업 상태가 만드는 중 또는 발송 중인 경우 작업을 취소할 수 있습니다.

**Hello Azure 포털에서에서 완료 된 작업의 hello 상태를 볼 수는 기간**

Too90 일 구성에 대 한 완료 된 작업에 대 한 hello 상태를 볼 수 있습니다. 90일이 지나면 완료된 작업이 삭제됩니다.

**Tooimport를 싶거나 내보내기 10 개 이상의 드라이브를 하는 경우 어떻게 해야 합니까?**

하나의 가져오기 또는 내보내기 작업 hello 가져오기/내보내기 서비스에 대 한 단일 작업에만 10 개 드라이브를 참조할 수 있습니다. 10 개 이상의 드라이브 tooship 하려는 경우에 여러 작업을 만들 수 있습니다. 같은 작업에서 함께 제공 해야 하는 hello와 연결 된 드라이브에는 동일한 패키지를 hello 합니다.
Microsoft는 데이터 용량이 여러 디스크 가져오기 작업에 걸쳐 있는 경우 지침과 지원을 제공합니다. 자세한 내용은 bulkimport@microsoft.com에게 문의하세요.

**가 서비스 반환 하기 전에 hello 드라이브를 포맷 hello?**

아니요. 모든 드라이브는 BitLocker로 암호화되어 있습니다.

**가져오기/내보내기 작업에 사용할 드라이브를 Microsoft에서 구입할 수 있습니까?**

아니요. 사용자는 자신의 드라이브 모두에 대 한 가져오기 및 내보내기 작업 tooship이 필요 합니다.

** 이 서비스를 통해 가져오는 데이터에 액세스하는 방법 **

Azure 저장소 계정에서 hello 데이터 hello Azure 포털을 통해 액세스할 수 있습니다 또는 저장소 탐색기 라는 독립 실행형 도구를 사용 하 여 합니다. https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer 

**Hello 가져오기 작업이 완료 된 후 어떤 됩니다 내 데이터 모양을 hello 저장소 계정에 있습니까? 디렉터리 계층 구조가 유지되나요?**

가져오기 작업을 위해 하드 드라이브를 준비할 때는 hello 대상은 데이터 집합 CSV에에서 hello DstBlobPathOrPrefix 필드에서 지정 됩니다. 이 hello 대상 컨테이너에서 hello 저장소 계정 toowhich hello 하드 드라이브에서 데이터를 복사 합니다. 이 대상 컨테이너에 있는 hello 하드 드라이브에서 폴더에 대 한 가상 디렉터리가 만들어집니다 및 blob 파일에 대해 생성 됩니다. 

**Hello 드라이브에 파일이 저장소 계정 내에 이미 있는 경우 hello 서비스가 덮어씁니다. 기존 blob 저장소 계정 내에서?**

Hello 대상 파일을 덮어쓸지 또는 hello 필드를 사용 하 여 처리를 호출 하는 데이터 집합 CSV 파일의 무시 여부를 hello 드라이브를 준비할 때는 지정할 수 있습니다: < 이름 바꾸기 | 아니요-덮어쓰기 | 덮어쓰기 > 합니다. 기본적으로 hello 서비스는 hello 새 파일 이름을 변경 되지 않고 기존 blob을 덮어씁니다.

**Hello WAImportExport 도구는 32 비트 운영 체제와 호환 되는?**
아니요. hello WAImportExport 도구 에서만 64 비트 Windows 운영 체제와 호환 됩니다. Hello에 toohello 운영 체제 섹션을 참조 하십시오 [필수](#pre-requisites) 전체 목록은 지원 되는 운영 체제 버전에 대 한 합니다.

**내 패키지에 hello 하드 디스크 드라이브 이외의 I를 포함 해야?**

하드 드라이브만 배송하고 전원 공급 장치 케이블이나 USB 케이블과 같은 품목은 포함하지 마세요.

**용량은 tooship FedEx 또는 DHL를 사용 하 여 내 드라이브**

FedEx, DHL, UPS 또는 미국 우편 서비스와 같은 모든 알려진된 운송 업체를 사용 하 여 드라이브 toohello 데이터 센터를 제공할 수 있습니다. 그러나, 배송 hello 드라이브 백 tooyou hello 데이터 센터에서 미국과 유럽, hello에 FedEx 계좌 번호 또는 hello 아시아 및 오스트레일리아의 경우 지역 DHL 계정 번호를 제공 해야 있습니다.

**국제적으로 드라이브를 발송하는 데 제한 사항이 있나요?**

전달 hello 실제 미디어 toocross 국경을 할 수 note 하십시오. 실제 미디어 및 데이터는 가져올 및/또는 되는지 hello 관련 법률에 따라 내보낸 것을 확인 합니다. 하기 전에 hello 실제 미디어 제공 되는 경우 확인 관리자 tooverify 미디어 및 데이터 식별 된 배송된 toohello 데이터 센터 수 합법적으로 있습니다. 이 경우에 Microsoft 적절 한 시기에 도달 tooensure를 도움이 됩니다.

**작업을 만들 때 hello 배달 주소는 내 저장소 계정 위치와에서 다른 위치. 어떻게 해야 하나요?**

일부 저장소 계정 위치는 매핑된 tooalternate 위치를 전달 합니다. 이전에 사용 가능한 배송 위치는 일시적으로 매핑된 tooalternate 위치 될 수도 있습니다. 항상 hello 배달 드라이브 배송 하기 전에 작업 생성 중에 제공 된 주소를 확인 합니다.

**드라이브를 배송할 때 hello carrier hello 데이터 센터 연락처 주소와 전화 번호를 요청 합니다. 무엇을 제공해야 하나요?**

전화 번호와 DC hello 주소 만들기 작업의 일부로 제공 됩니다.

**Hello Azure 가져오기/내보내기 서비스 toocopy PST 사서함과 SharePoint 데이터 tooO365를 사용할 수 있습니까?**

너무를 참조 하십시오[가져오기 PST 파일이 나 SharePoint 데이터 tooOffice 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx)합니다.

**사용할 수 hello Azure 가져오기/내보내기 서비스 toocopy 내 백업을 오프 라인 toohello Azure 백업 서비스?**

너무를 참조 하십시오[Azure 백업에서 오프 라인 백업 워크플로](../backup/backup-azure-backup-import-export.md)합니다.

**Hello 최대 수에 대 한 HDD 되거나 하나의 배송에 이란?**

Hdd 개수에 관계 없이 되거나 하나의 배송에 있을 수 있으며 권장 hello 디스크 toomultiple 작업 속하면는 너무) hello 해당 작업 이름으로 레이블이 지정 된 hello 디스크. -1, 그 뒤에 추적 번호를 가진 b) 업데이트 hello 작업-2 등입니다.
  
**Hello 최대 블록 Blob 및 페이지 Blob 크기 디스크 가져오기/내보내기에서 지원 되는 것이 무엇입니까?**

최대 블록 Blob 크기는 약 4.768TB 또는 5,000,000MB입니다.
최대 페이지 Blob 크기는 1TB입니다.

**디스크 Import/Export는 AES 256 암호화를 지원하나요?**

AES 128 bitlocker 암호화와 함께 기본적으로 azure 가져오기/내보내기 서비스를 암호화 하지만 수동으로 데이터를 복사 하기 전에 bitlocker로 암호화 하 여 증가 된 tooAES 256 될 수 있습니다. 

[WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip)을 사용하는 경우 샘플 명령은 아래와 같습니다.
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
사용 하는 경우 [WAImportExport 도구](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) "AlreadyEncrypted"를 지정 하 고 hello driveset CSV의에서 hello 키를 제공 합니다.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>다음 단계

* [Hello WAImportExport 도구 설정](storage-import-export-tool-how-to.md)
* [Hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송 합니다.](storage-use-azcopy.md)
* [Azure Import/Export REST API 샘플](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

