---
title: "Windows 스토어 앱에서 Azure 저장소 aaaUse | Microsoft Docs"
description: "Windows 저장 하는 toocreate 방법에 대해 알아봅니다 Azure Blob, 큐, 테이블 또는 파일 저장소를 사용 하는 응용 프로그램입니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>어떻게 Windows 스토어 앱에서 Azure 저장소 toouse
## <a name="overview"></a>개요
이 가이드에서 Azure 저장소를 활용 하는 Windows 스토어 앱 개발 tooget 시작 하는 방법을 보여 줍니다.

## <a name="download-required-tools"></a>필요한 도구 다운로드
* [Visual Studio](https://www.visualstudio.com/downloads/) 쉽게 toobuild를 사용 하면 디버그, 지역화, 패키지 및 Windows 스토어 앱을 배포 합니다. Visual Studio 2012 이상이 필요합니다.
* hello [Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage) Azure 저장소를 사용 하기 위한 Windows 런타임 클래스 라이브러리를 제공 합니다.
* [WCF 데이터 서비스 도구 Windows 스토어 앱 용](http://www.microsoft.com/download/details.aspx?id=30714) Visual Studio에서 Windows 스토어 앱에 대 한 클라이언트 쪽 OData 지 원하는 hello 서비스 참조 추가 경험을 확장 합니다.

## <a name="develop-apps"></a>앱 개발
### <a name="getting-ready"></a>준비
Visual Studio 2012 이상에서 새 Windows 스토어 앱 프로젝트를 만듭니다.

![store-apps-storage-vs-project][store-apps-storage-vs-project]

다음으로, 마우스 오른쪽 단추로 클릭 하 여 참조 toohello Azure 저장소 클라이언트 라이브러리를 추가 **참조**, **참조 추가**, 다음 toohello Windows Runtime 용 저장소 클라이언트 라이브러리를 검색 하 고 있는 다운로드:

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>Hello Blob로 hello 라이브러리 및 큐 서비스를 사용 하 여
이 응용 프로그램 준비 toocall hello Azure Blob 및 큐 서비스입니다. Hello 다음 추가 **를 사용 하 여** 문의 하 여 Azure 저장소 형식을 직접 참조할 수 있습니다.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

다음으로 단추 tooyour 페이지를 추가 합니다. 다음 코드 tooits hello 추가 **클릭** 이벤트 hello를 사용 하 여 이벤트 처리기 메서드를 수정 하 고 [async 키워드](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

이 코드에서는 두 개의 문자열 변수인 *accountName* 및 *accountKey*가 있다고 가정합니다. 저장소 계정 및 hello 계정 키의 해당 계정에 연관 된 hello 이름을 나타냅니다.

빌드하고 hello 응용 프로그램을 실행 합니다. Hello 단추를 클릭 하는 컨테이너 이름을 지정 여부를 확인 *container1* 계정에 있으며 다음 없으면 만듭니다.

### <a name="using-hello-library-with-hello-table-service"></a>Hello 라이브러리를 사용 하 여 테이블 서비스 hello로
Windows 스토어 응용 프로그램 라이브러리 hello에 대 한 WCF Data Services에 hello Azure 테이블 서비스와 함께 사용 되는 toocommunicate 않은 형식에 따라 다릅니다. 다음으로, 참조 toohello WCF 라이브러리를 사용 하 여 hello 패키지 관리자 콘솔이 필요한 추가:

![store-apps-storage-package-manager][store-apps-storage-package-manager]

사용 하 여 hello 다음 명령은 toopoint 컴퓨터의 패키지 관리자 toohello 위치:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

이 명령은 모든 필요한 참조 tooyour 프로젝트를 자동으로 추가 됩니다. Toouse 하지 않을 경우 패키지 관리자 콘솔 hello, 로컬 컴퓨터 toohello 패키지 소스 목록에 hello WCF Data Services NuGet 폴더에 추가 하 고 다음에 설명 된 대로 hello UI 통해 hello 참조를 추가할 수 [관리 NuGet 패키지를 사용 하 여 hello 대화](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)합니다.

Hello WCF Data Services NuGet 패키지를 참조 하는 경우 프로그램 단추에 hello 코드 변경 **클릭** 이벤트:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

이 코드는 *table1* 이라는 테이블이 계정이 있는지 확인하고 없으면 새로 만듭니다.

또한 동일한 패키지를 다운로드 하는 hello에서 사용 하지 않는 참조 tooMicrosoft.WindowsAzure.Storage.Table.dll을 추가할 수 있습니다. 이 라이브러리에는 리플렉션 기반 직렬화 및 일반 쿼리와 같은 추가 기능이 포함되어 있습니다. 이 라이브러리는 JavaScript를 지원하지는 않습니다.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
