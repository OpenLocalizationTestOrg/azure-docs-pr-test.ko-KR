---
title: "aaaDeciding 때 toouse Azure Blob, Azure 파일 또는 Azure 데이터 디스크"
description: "어떤 기술을 toouse 결정 toohelp Azure의 hello 다양 한 방법 toostore 및 액세스 데이터에 알아봅니다."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: 6109affe41e98ed459616a4f91064ded0c74428d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>결정할 때 toouse Azure Blob, Azure 파일 또는 Azure 데이터 디스크

Microsoft Azure hello 클라우드에서 사용자 데이터 저장 및 액세스에 대 한 Azure 저장소의 몇 가지 기능을 제공 합니다. 이 문서는 Azure 파일, Blob 및 데이터 디스크에 설명 하 고은 설계 된 toohelp 이러한 기능 중에서 선택할 수 있습니다.

## <a name="scenarios"></a>시나리오

다음 표에서 hello 파일, Blob 및 데이터 디스크를 비교 하 여 각각에 대해 적절 한 예제 시나리오를 보여 줍니다.

| 기능 | 설명 | 때 toouse |
|--------------|-------------|-------------|
| **Azure 파일** | 클라이언트 라이브러리에서 SMB 인터페이스를 제공 및 [REST 인터페이스](/rest/api/storageservices/file-service-rest-api) toostored 파일 어디에서 나 액세스할 수 있습니다. | 너무 리프트 "및" 시프트 원하는 이미 Azure에서 실행 중인 다른 응용 프로그램 간의 hello 네이티브 파일 시스템 Api tooshare 데이터를 사용 하는 응용 프로그램 toohello 클라우드가 있습니다.<br/><br/>Toostore 개발 및 디버깅 도구 toobe 많은 가상 컴퓨터에서 액세스 해야 하는 것이 좋습니다. |
| **Azure Blob** | 클라이언트 라이브러리를 제공 및 [REST 인터페이스](/rest/api/storageservices/blob-service-rest-api) 구조화 되지 않은 데이터를 허용 하는 저장 및 블록 blob에서 대규모로 액세스 너무 합니다. | 응용 프로그램 toosupport 스트리밍 및 임의 액세스 시나리오는 것이 좋습니다.<br/><br/>어디에서 든 toobe 수 tooaccess 응용 프로그램 데이터 사용 하는 것이 좋습니다. |
| **Azure 데이터 디스크** | 클라이언트 라이브러리를 제공 및 [REST 인터페이스](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) 데이터 toobe 영구적으로 저장 하 고 연결된 된 가상 하드 디스크에서 액세스할 수 있도록 합니다. | Toolift 한 네이티브 파일 시스템 Api tooread 사용 하며 데이터 toopersistent 디스크를 작성 하는 응용 프로그램을 이동 합니다.<br/><br/>필요한 toobe 외부 hello 가상 컴퓨터 toowhich hello 디스크에서 액세스 하지 않은 toostore 데이터가 연결 된 것이 좋습니다. |

## <a name="comparison-files-and-blobs"></a>비교: 파일 및 Blob

다음 표에서 hello Azure 파일과 Azure Blob을 비교 합니다.  
  
||||  
|-|-|-|  
|**특성**|**Azure Blob**|**Azure 파일**|  
|내구성 옵션|LRS, ZRS, GRS(높은 가용성을 위해서는 RA-GRS)|LRS, GRS|  
|접근성|REST API|REST API<br /><br /> SMB 2.1 및 SMB 3.0(표준 파일 시스템 API)|  
|연결|REST APIs -- 전 세계|REST APIs - 전 세계<br /><br /> SMB 2.1 -- 지역 내<br /><br /> SMB 3.0 -- 전 세계|  
|끝점|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|디렉터리|단일 구조 네임스페이스|실제 디렉터리 개체|  
|이름 대/소문자 구분|대/소문자 구분|대/소문자 구분 안 함, 대/소문자 유지|  
|용량|Too500 500TB 컨테이너를|5TB 파일 공유|  
|처리량|블록 blob 당 too60 MB/s를|공유 당 too60 MB/s를|  
|개체 크기|Too200 g B/블록 blob을|Too1TB/파일을|  
|요금 청구 용량|기록된 바이트 기준|파일 크기 기준|  
|클라이언트 라이브러리|여러 언어|여러 언어|  
  
## <a name="comparison-files-and-data-disks"></a>비교: 파일 및 데이터 디스크

Azure 파일은 Azure 데이터 디스크를 보완합니다. 데이터 디스크는 한 번에 연결 된 tooone Azure 가상 컴퓨터 수만 있습니다. 데이터 디스크는 고정 형식의 vhd를 Azure 저장소에 페이지 blob으로 저장 하 고 hello 가상 컴퓨터 toostore 영 속 데이터에서 사용 됩니다. Azure 파일에서 파일 공유에 액세스할 수 있습니다에 hello 동일한 방식으로 hello 로컬 디스크 (기본 파일 시스템 Api 사용)에서 액세스 하 고 여러 가상 컴퓨터에서 공유할 수 있습니다.  
 
다음 표에서 hello Azure 파일과 Azure 데이터 디스크를 비교 합니다.  
 
||||  
|-|-|-|  
|**특성**|**Azure 데이터 디스크**|**Azure 파일**|  
|범위|단독 tooa 단일 가상 컴퓨터|여러 가상 컴퓨터 간에 공유 액세스|  
|스냅숏 및 복사|예|아니요|  
|구성|Hello 가상 컴퓨터 시작 시 연결 됨|Hello 가상 컴퓨터가 시작 후에 연결 됨|  
|인증|기본 제공|net use로 설정|  
|정리|자동|설명서|  
|REST를 사용하여 액세스|Hello VHD 내의 파일에 액세스할 수 없습니다.|공유에 저장된 파일에 액세스할 수 있음|  
|최대 크기|1TB 디스크|공유 내 5TB 파일 공유 및 1TB 파일|  
|최대 8KB IOps|500IOps|1000IOps|  
|처리량|디스크당 too60 MB/s를|파일 공유 단위로 too60 m B/초|  

## <a name="next-steps"></a>다음 단계

데이터 저장 및 액세스 방법을 결정할 때는 고려해 야 hello 비용 관련 된. 자세한 내용은 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.
  
일부 SMB 기능은 해당 toohello 클라우드 수 있습니다. 자세한 내용은 참조 [hello Azure 파일 서비스에서 지원 되지 않는 기능](/rest/api/storageservices/features-not-supported-by-the-azure-file-service)합니다.
  
데이터 디스크에 대 한 자세한 내용은 참조 [디스크 및 이미지 관리](storage-about-disks-and-vhds-linux.md) 및 [어떻게 tooAttach 데이터 디스크 tooa Windows 가상 컴퓨터](../virtual-machines/windows/classic/attach-disk.md)합니다.
