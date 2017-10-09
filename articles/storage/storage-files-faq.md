---
title: "Azure 파일 저장소에 대 한 질문과 aaaFrequently | Microsoft Docs"
description: "찾기 toofrequently Azure 파일 저장소에 대 한 질문과 대답을 제공 합니다."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: ecd685b3094f51e998bbf5dd0567a20732757015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Azure File Storage 보안에 대한 FAQ(질문과 대답)

## <a name="general"></a>일반
* **Q. Azure File Storage란?**  
   
    Azure File Storage는 Azure의 분산 파일 시스템입니다. 지원 되는 Azure 가상 컴퓨터 또는 온-프레미스 컴퓨터에 있는 네이티브 공유로 사용자 toomount hello 저장소 수 있는 SMB 프로토콜 인터페이스를 제공 합니다.

* **Q. Azure File Storage가 유용한 이유는 무엇인가요?**  
   
    Azure File Storage는 여러 VM 및 플랫폼 간에 공유 데이터 액세스를 제공합니다. 너무 참조[이유 Azure 파일 저장소는 유용](storage-files-introduction.md#why-azure-file-storage-is-useful)합니다.

* **Q. Azure File, Azure Blob 및 Azure Disk는 언제 사용해야 하나요?**  
   
    Microsoft Azure hello 클라우드에서 toostore 및 액세스 데이터를 여러 가지 방법으로 제공합니다.  
   
    Azure 파일 저장소-SMB 인터페이스, 클라이언트 라이브러리 및 toostored 파일 어디에서 든 쉽게 액세스할 수 있도록 REST 인터페이스를 제공 합니다.  
   
    Azure Blob-클라이언트 라이브러리 및 구조화 되지 않은 데이터 toobe 저장 하 고 블록 blob에서 대규모로 액세스를 허용 하는 REST 인터페이스를 제공 합니다.  
   
    Azure 데이터 디스크-클라이언트 라이브러리 및 데이터 toobe 영구적으로 저장 하 고 연결된 된 가상 하드 디스크에서 액세스를 허용 하는 REST 인터페이스를 제공 합니다.  
   
    자세히 알아보세요 [결정 때 toouse Azure Blob, Azure 파일 또는 Azure 데이터 디스크](storage-decide-blobs-files-disks.md)

* **Q. Azure File Storage로 시작하려면 어떻게 해야 하나요?**  
   
    Azure 파일 공유를 만들어 시작할 수 있습니다. Azure 포털 "," hello Azure 저장소 PowerShell cmdlet "," hello Azure 저장소 클라이언트 라이브러리 "또는" hello Azure 저장소 REST API를 사용 하 여 Azure 파일 공유를 만들 수 있습니다. 이 자습서에서는 배웁니다.

    * [Hello 포털을 사용 하 여 toocreate Azure 파일을 공유 하는 방법에 대해 알아봅니다](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Powershell을 사용 하 여 toocreate Azure 파일을 공유 하는 방법에 대해 알아봅니다](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [CLI를 사용 하 여 toocreate Azure 파일을 공유 하는 방법에 대해 알아봅니다](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **Q. Azure File Storage는 어떤 복제를 지원하나요?**  
   
    Azure File Storage는 현재 LRS 또는 GRS만 지원합니다. RA-GRS toosupport 계획 있지만 아직 타임 라인 tooshare 되지 않습니다.

## <a name="security-authentication-and-access-control"></a>보안, 인증 및 액세스 제어

* **Q. Azure 파일 저장소의 다양 한 방법 tooaccess 파일 이란?**
    
    SMB 3.0 프로토콜을 사용 하 여 로컬 컴퓨터의 hello 파일 공유를 탑재할 수 또는 사용 하 여 도구와 같은 [저장소 탐색기](http://storageexplorer.com/) 파일 공유의 tooaccess 파일입니다. 응용 프로그램에서 저장소 클라이언트 라이브러리, REST Api 또는 Powershell tooaccess Azure 파일의 파일 공유를 사용할 수 있습니다.

* **Q. 웹 브라우저를 사용 하 여 액세스 tooa 특정 파일을 제공 하려면 어떻게 해야 합니까?**
    
    SAS를 사용하면 지정된 시간 간격 동안 유효한 특정 권한을 가진 토큰을 생성할 수 있습니다. 예를 들어 특정 시간 동안에 대 한 읽기 전용 액세스 tooa 특정 파일이 있는 토큰을 생성할 수 있습니다. 가 유효한 동안 모든 웹 브라우저에서 직접 hello 파일에 액세스할 수 있습니다이 url을 소유한 모든 사용자. 저장소 탐색기 같은 UI에서 SAS 키를 쉽게 생성할 수 있습니다.

* **Q. Hello 공유 내 폴더에 읽기 전용 이거나 쓰기 전용 권한을 가능한 toospecify 입니까?**
    
    SMB 통해 hello 파일 공유를 탑재 하는 경우 사용 권한 보다 이러한 제어 수준은 필요는 없습니다. 그러나 hello REST API를 통해 공유 액세스 서명 (SAS) 또는 클라이언트 라이브러리를 만들어이 작업을 수행할 수 있습니다.  

* **Q. Azure File Storage에 대한 서버 쪽 암호화를 사용하려면 어떻게 해야 하나요?**

    Azure File Storage에 대한 [서버 쪽 암호화](storage-service-encryption.md)는 일반적으로 모든 지역과 공용 및 국가별 클라우드에서 사용할 수 있습니다. [Azure Portal](https://portal.azure.com/), [Microsoft Azure Storage 리소스 공급자 API](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) 또는 [Azure CLI](storage-azure-cli.md)를 사용하여 Azure File Storage에 대한 SSE를 사용하도록 설정할 수 있습니다.
    
    Azure 파일 저장소에 SSE을 활성화 한 다음 해당 저장소 계정 toohello 파일 저장소로 작성 된 새 데이터도 자동으로 암호화 됩니다. 이 기능은 tooexisting 또는 새 공유는 기존 또는 새 저장소 계정에 작성 된 모든 새 데이터에 사용할 수 있습니다. 이 기능을 사용하는 추가 비용은 없습니다. 자세히 알아보세요 [어떻게 Azure 파일 저장소에 SSE tooenable](storage-service-encryption.md)합니다.

* **Q. Azure File Storage에서 Active Directory 기반 인증을 지원하나요?**
   
    우리는 현재 AD 기반 인증 또는 ACL을 지원하지 않지만 우리의 기능 요청 목록에 해당 기능을 포함합니다. 지금은 hello Azure 저장소 계정 키 사용된 tooprovide 인증 toohello 파일 공유 됩니다. 공유 액세스 서명 (SAS)를 사용 하 여 hello REST API 또는 hello 클라이언트 라이브러리를 통해 해결 방법이 제공지 않습니다. SAS를 사용하면 지정된 시간 간격 동안 유효한 특정 권한을 가진 토큰을 생성할 수 있습니다. 예를 들어 10 분 동안 만료 된 파일을 지정 하는 읽기 전용 액세스 tooa와 토큰을 생성할 수 있습니다. 가 유효한 동안이 토큰을 소유한 모든 사용자에 해당 10 분에 대 한 읽기 전용 액세스 toothat 파일이 있습니다.
   
    SAS는 hello REST API 또는 클라이언트 라이브러리를 통해 지원 됩니다. Hello SMB 프로토콜을 통해 hello 파일 공유를 탑재할 때 SAS toodelegate 액세스 tooits 콘텐츠를 사용할 수 없습니다. 
    
* **Q. Azure 파일 저장소에 대 한 지원 hello 데이터 규정 준수 정책 이란?**

   Azure 파일 저장소 실행의 맨 위에 다른 저장소에서 Azure 저장소 서비스 및 hello 적용 동일한 저장소 아키텍처를 hello 동일한 데이터 규정 준수 정책입니다. Azure 저장소 데이터 규정 준수에 대 한 자세한 내용은 다운로드 하 고 수 너무 참조[Microsoft Azure 데이터 보호 문서](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409)합니다.

## <a name="on-premises-access"></a>온-프레미스 액세스

* **Q.Do toouse Azure express 경로 tooconnect tooAzure 파일 저장소는 온-프레미스 VM에서 있습니까?**
   
    아니요. Express 경로 설정 하지 않은 경우 계속 액세스할 수 있습니다 hello 파일 공유 온-프레미스에서 포트 445 (TCP 아웃 바운드) 인터넷 액세스에 대 한 열기를 보유 합니다. 그러나 원하는 경우 파일 저장소와 함께 ExpressRoute를 사용할 수 있습니다.

* **Q. 내 로컬 컴퓨터에서 Azure 파일 공유를 탑재하려면 어떻게 해야 하나요?** 
    
    포트 445 (TCP 아웃 바운드)이 열려 있고 클라이언트 hello SMB 3.0 프로토콜을 지 원하는 hello SMB 프로토콜을 통해 hello 파일 공유를 탑재할 수 있습니다 (예를 들어 사용할 Windows 10 또는 Windows Server 2012). 로컬 ISP 공급자 toounblock hello 포트를 사용 하십시오. 중간 hello에서 사용 하 여 파일을 볼 수 있습니다 [저장소 탐색기](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents)합니다.


## <a name="billing-and-pricing"></a>가격 및 대금 청구
* **Q. 가 toohello 구독 청구 되는 외부 대역폭으로 파일 공유 수와 Azure VM 간의 네트워크 트래픽이 hello?**
   
    Hello 파일 공유 및 VM에 있으면 hello 같은 Azure 지역 hello 서로 트래픽이 무료입니다. 다른 지역에 있으면 둘 사이의 hello 트래픽 외부 대역폭으로 청구 됩니다.

## <a name="backup"></a>백업

* **Q. 내 Azure 파일 공유를 백업하려면 어떻게 하나요?**
    
    탑재된 파일 공유를 백업할 수 있는 AzCopy, RoboCopy 또는 타사 백업 도구를 사용할 수 있습니다. Hello 가까운 미래;에서 파일 공유의 toohave hello 기능 tootake 스냅숏을 예상합니다 수 toouse 됩니다.이 기능은 toobackup Azure 파일을 공유 합니다.

## <a name="performance"></a>성능

* **Q. Azure 파일 저장소의 규모 제한을 hello 이란?**
    Azure File Storage의 확장성 및 성능 목표에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files)를 참조하세요.

* **Q. Azure 파일 저장소로 toounzip 파일을 동안 내 성능 느린 했습니다. 어떻게 해야 하나요?**
    
    많은 수의 Azure 파일 저장소에 파일 tootransfer, 이러한 도구에 대 한 네트워크 전송을 최적화 하는 대로 AzCopy (Windows, Linux/Unix에 대 한 미리 보기) 또는 Azure Powershell을 사용 하는 것이 좋습니다.

* **Q. 되었습니다 패치 toofix 속도가 느린 성능 문제를 Azure 파일 저장소?**
    
    Windows 팀 hello hello 고객 Windows 8.1 또는 Windows Server 2012 r 2에서 Azure 파일 저장소에 액세스 하는 경우 패치 toofix를 성능 저하 문제 최근에 릴리스 했습니다. 자세한 내용은 하십시오 체크 아웃 hello 관련 된 기술 자료 문서 [Windows 8.1 또는 Server 2012 r 2에서 Azure 파일 저장소에 액세스할 때 성능이 저하](https://support.microsoft.com/kb/3114025)합니다.

## <a name="features-and-interoperability-with-other-services"></a>다른 서비스와의 기능 및 상호 운용성
* **Q. Azure 파일 저장소에 대 한 "파일 공유 감시" hello 중 하나로 장애 조치 클러스터에 대 한 사용 사례는?**
   
    현재 지원되지 않습니다.

* **Q. Hello REST API에는 이름 바꾸기 작업 거기?**
   
    지금은 없습니다.

* **Q. 중첩된 공유, 즉 공유 아래에 공유를 가질 수 있나요?**
    
    아니요. hello 파일 공유를 탑재 하는 가상 드라이버 hello 이므로 중첩된 공유는 지원 되지 않습니다.

* **Q. IBM MQ에서 Azure File Storage를 사용하고 있습니다.**
    
    해당 서비스와 Azure 파일 저장소를 구성할 때 IBM 문서 tooguide IBM MQ 고객을 릴리스 했습니다. 자세한 내용은 확인 하세요 [어떻게 toosetup IBM MQ 다중 인스턴스 큐 관리자와 Microsoft Azure 파일 서비스](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service)합니다.


## <a name="troubleshooting"></a>문제 해결
* **Q. Azure File Storage 오류를 어떻게 해결하나요?**
    
    너무 참조할 수[Azure 파일 저장소 문제 해결 문서](storage-troubleshoot-file-connection-problems.md) 종단 간 문제 해결 지침에 대 한 합니다. 


## <a name="see-also"></a>참고 항목
Azure 파일 저장소에 대한 자세한 내용은 다음 링크를 참조합니다.

### <a name="conceptual-articles-and-videos"></a>개념 문서 및 비디오
* [Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [어떻게 toouse Linux로 Azure 파일 저장소](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>파일 저장소용 도구 지원
* [Azure 저장소와 함께 Azure PowerShell 사용](storage-powershell-guide-full.md)
* [어떻게 toouse AzCopy Microsoft Azure 저장소](storage-use-azcopy.md)
* [Hello Azure CLI를 사용 하 여 Azure 저장소](storage-azure-cli.md)
* [Azure File Storage 문제 해결](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a>블로그 게시물
* [Azure 파일 저장소 일반적으로 사용 가능(영문)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure File Storage 내부 구조(영문)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure 파일 서비스 소개](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [마이그레이션 데이터 tooAzure 파일 저장소](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>참조
* [Storage Client Library for .NET 참조](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [파일 서비스 REST API 참조](http://msdn.microsoft.com/library/azure/dn167006.aspx)
