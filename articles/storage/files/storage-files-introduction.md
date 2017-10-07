---
title: "파일 저장소 aaaIntroduction tooAzure | Microsoft Docs"
description: "소개 tooAzure 네트워크 파일을 제공 하는 파일 저장소를 공유 하는 Microsoft 클라우드 hello에서"
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
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: fe6826e79c364a6956831d2e273c4342a5fd47f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>소개 tooAzure 파일 저장소

Azure 파일 저장소 네트워크 파일 공유를 hello 업계 표준을 사용 하 여 hello 클라우드 제공 [서버 메시지 블록 (SMB) 프로토콜](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) 및 [파일 시스템 CIFS (Common Internet)](https://technet.microsoft.com/library/cc939973.aspx)합니다. Azure 파일 공유는 Windows, macOS, Linux를 실행하는 Azure Virtual Machines 또는 온-프레미스 환경에서 동시에 탑재할 수 있습니다. TooAzure 파일 저장소, Azure Blob 저장소 및 Azure 큐 저장소를 액세스할 수는 일반적인 용도의 스토리지 계정 있습니다.

## <a name="videos"></a>비디오
| Azure File Storage 소개(27분) | Azure File Storage 자습서(5분)  |
|-|-|
| [![Hello 소개 Azure 파일 저장소 비디오-동영상 가이드 tooplay 클릭 하세요.](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Hello Azure 파일 저장소 자습서-동영상 가이드 tooplay 클릭 하세요.](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Azure File Storage가 유용한 이유

Azure 파일 저장소 있습니다 tooreplace Windows Server, Linux 또는 NAS 기반 파일 서버 온-프레미스 호스팅되거나 hello 클라우드의 클라우드 OS 필요 없는 파일 공유. Azure 파일 저장소 hello 이점을 뒤에 있습니다.

* **공유 액세스** Azure 파일 수 있음을 의미 하는 표준 SMB 프로토콜을 완벽 하 게으로 바꿀 수 온-프레미스 파일 공유 Azure 파일 공유 응용 프로그램 호환성에 대 한 걱정 없이 지원 hello 업계를 공유 합니다. 수 tooaccess 여러 응용 프로그램/인스턴스 및 컴퓨터에서 파일 공유는 Azure 파일 저장소와 중요 한 장점입니다.

* **완전히 관리** hello 필요 toomanage 하드웨어 또는 OS hello 서버 운영 체제 업그레이드 시 중요 한 보안 패치 또는 결함이 있는 하드 디스크를 바꾸는 toodeal 없는 즉 없이 Azure 파일 공유를 만들 수 있습니다.

* **스크립팅 및 Tooling** PowerShell cmdlet 및 Azure CLI 사용된 toocreate 수 탑재 하 고 Azure 응용 프로그램의 hello 관리의 일부로 Azure 파일 공유를 관리 합니다. 만들고 hello를 사용 하 여 Azure 파일 공유를 관리할 수 [Azure 포털](https://portal.azure.com) 및 hello [Azure 저장소 탐색기](https://storageexplorer.com)합니다. 

* **복원 력** Azure 파일 저장소를 항상 사용 가능 toobe 접지 hello에서 빌드된 합니다. Azure 파일 경로로 바꿉니다 온-프레미스 파일 공유 저장소 toowake toodeal 로컬 정전 또는 네트워크 문제를 더 이상 없을 의미 합니다. 

* **친숙 한 프로그래밍** Azure에서 실행 중인 응용 프로그램을 통해 hello 공유의 데이터에 액세스할 수 [파일 I/O Api 시스템](https://msdn.microsoft.com/library/system.io.file.aspx)합니다. 개발자는 기존 코드 및 기술 toomigrate 기존 응용 프로그램에 따라서 활용할 수 있습니다. 또한 tooSystem IO Api를 사용할 수 있습니다 하나 hello 같은 hello Azure 저장소 클라이언트 라이브러리 중 하나에 대 한 [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet), 또는 hello [Azure 저장소 REST API](/rest/api/storageservices/file-service-rest-api)합니다.

Azure 파일 공유를 사용하여 다음을 수행할 수 있습니다.

* **Replace 온-프레미스 파일 서버** Azure 파일 저장소에는 기존의 온-프레미스 파일 서버 또는 NAS 장치에서 사용 되는 toocompletely 바꾸기 파일 공유 일 수 있습니다. 쉽게 창과 macOS 등 Linux와 같은 인기 있는 운영 체제 수 hello world 있든지 Azure 파일 공유를 탑재 해야 합니다.

* **응용 프로그램 "전환"**

    Azure 파일 저장소를 사용 하면 온-프레미스 파일을 사용 하는 응용 프로그램 toohello 클라우드 "리프트 및 이동" hello 응용 프로그램의 부분 간에 tooshare 데이터를 공유 하는 너무 쉽게 합니다. tooimplement이 각 VM toohello 파일 공유를 연결 하 고 읽고 그 온-프레미스 파일에 대해 공유 하는 것 처럼 파일을 쓸 수 다음 합니다.

* **클라우드 개발 간소화**
    
    Azure 파일 저장소의 여러 가지 방법으로 toosimplify 새 클라우드 개발 프로젝트에에서 사용할 수 있습니다.
    
    * **공유 응용 프로그램 설정**
    
        분산된 응용 프로그램에 대 한 일반적인 패턴은 여러 다른 Vm에서 액세스할 수 있는 중앙된 위치에 toohave 구성 파일입니다. 이제 이러한 구성 파일을 Azure 파일 공유에 저장하고 모든 응용 프로그램 인스턴스에서 읽을 수 있습니다. 이러한 설정은 hello REST 인터페이스를 통해 전 세계 액세스 toohello 구성 파일을 통해 관리할 수도 있습니다.

    * **진단 공유**
    
        Azure 파일 공유에는 로그, 메트릭 및 크래시 덤프와 같은 진단 파일을 사용 하는 toosave 될 수도 있습니다. 파일 공유에 SMB hello와 REST 인터페이스를 통해 사용할 수 있는 응용 프로그램 toobuild를 허용 하거나 다양 한 처리 및 hello 진단 데이터를 분석 하기 위한 분석 도구를 활용 합니다.

    * **개발/테스트/디버그**

        개발자 또는 관리자 hello 클라우드에서 Vm에서 작업, 도구 또는 유틸리티 집합이 자주 필요 합니다. 필요로 하는 각 가상 컴퓨터에 이러한 유틸리티를 설치 및 배포하는 데에는 시간이 많이 걸릴 수 있습니다. Azure 파일 저장소 개발자 또는 관리자에 저장할 수 선호 하는 도구 toofrom 쉽게 연결된 될 수 있는 파일 공유에 있는 가상 컴퓨터.
        
## <a name="how-does-it-work"></a>작동 원리

Azure 파일 공유 관리는 온-프레미스 파일 공유 관리보다 훨씬 간단합니다. 다이어그램을 다음 hello hello Azure 파일 저장소 관리 구문을 보여 줍니다.

![파일 구조](./media/storage-files-introduction/files-concepts.png)

* **저장소 계정** 저장소 계정을 통해 모든 액세스 tooAzure 저장소 작업은 수행 됩니다. 저장소 계정 용량에 대한 자세한 내용은 [확장성 및 성능 목표](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)를 참조하세요.

* **공유** File Storage 공유는 Azure의 SMB 파일 공유입니다. 모든 디렉터리 및 파일을 부모 공유에 만들어야 합니다. 계정에 공유를 개수에 제한 없이 포함 될 수 있습니다 및 공유 파일 toohello 5TB hello 파일 공유의 총 용량을 개수에 제한 없이 저장할 수 있습니다.

* **디렉터리** 선택적인 디렉터리 계층 구조입니다.

* **파일** hello 공유에 있는 파일입니다. 파일 크기가 too1 TB up 될 수 있습니다.

* **URL 형식** 파일은 URL 형식에 따라 hello를 사용 하 여 주소를 지정할 수 있습니다.  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```

## <a name="next-steps"></a>다음 단계

* [Azure 파일 공유 만들기](storage-how-to-create-file-share.md)
* [Windows에 연결 및 탑재](storage-how-to-use-files-windows.md)
* [Linux에 연결 및 탑재](storage-how-to-use-files-linux.md)
* [macOS에 연결 및 탑재](storage-how-to-use-files-mac.md)
* [FAQ](../storage-files-faq.md)
* [Windows에서 문제 해결](storage-troubleshoot-windows-file-connection-problems.md)   
* [Linux에서 문제 해결](storage-troubleshoot-linux-file-connection-problems.md)   

<!-- Rena I would remove any articles from here that are more than a year old. - Robin-->
### <a name="conceptual-articles-and-videos"></a>개념 문서 및 비디오
* [Azure File Storage: 원활한 Windows 및 Linux용 클라우드 SMB 파일 시스템(영문)](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Azure File Storage용 도구 지원
* [어떻게 toouse AzCopy Microsoft Azure 저장소](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Hello Azure CLI를 사용 하 여 Azure 저장소](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)

### <a name="blog-posts"></a>블로그 게시물
* [Azure 파일 저장소 일반적으로 사용 가능(영문)](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure File Storage 내부 구조(영문)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure 파일 서비스 소개](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [마이그레이션 데이터 tooAzure 파일](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>참조
* [Storage Client Library for .NET 참조](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [파일 서비스 REST API 참조](http://msdn.microsoft.com/library/azure/dn167006.aspx)
