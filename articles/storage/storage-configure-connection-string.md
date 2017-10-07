---
title: "Azure 저장소에 대 한 연결 문자열 aaaConfigure | Microsoft Docs"
description: "Azure Storage 계정에 대한연결 문자열을 구성합니다. 연결 문자열에 필요한 tooauthenticate tooa 저장소 계정에 액세스 런타임에 응용 프로그램에서 hello 정보가 포함 됩니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a>Azure Storage 연결 문자열 구성

연결 문자열에는 런타임 시에 Azure 저장소 계정에 응용 프로그램 tooaccess 데이터에 필요한 hello 인증 정보가 포함 됩니다. 다음과 같은 작업을 수행하도록 연결 문자열을 구성할 수 있습니다.

* Toohello Azure 저장소 에뮬레이터를 연결 합니다.
* Azure의 저장소 계정에 액세스
* SAS(공유 액세스 서명)를 통해 Azure의 지정된 리소스에 액세스

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>사용자의 연결 문자열 저장
응용 프로그램에 런타임 tooauthenticate 요청이 tooAzure 저장소에서 tooaccess hello 연결 문자열이 필요합니다. 연결 문자열을 저장하기 위한 여러 가지 옵션이 있습니다.

* Hello 바탕 화면이 나 장치에서 응용 프로그램 실행 하는 hello 연결 문자열에 저장할 수는 **app.config** 또는 **web.config** 파일입니다. 추가 연결 문자열 toohello hello **AppSettings** 이러한 파일의 섹션입니다.
* Azure 클라우드 서비스에서 실행 중인 응용 프로그램 hello에 hello 연결 문자열을 저장할 수 [Azure 서비스 구성 스키마 (.cscfg) 파일](https://msdn.microsoft.com/library/ee758710.aspx)합니다. 추가 연결 문자열 toohello hello **ConfigurationSettings** hello 서비스 구성 파일의 섹션입니다.
* 사용자 코드에서 직접 연결 문자열을 사용할 수 있습니다. 그러나 대부분의 시나리오에서 구성 파일에 연결 문자열을 저장하는 것이 좋습니다.

연결 문자열은 구성 파일에 저장 하면 쉽게 tooupdate hello 연결 문자열 tooswitch hello 저장소 에뮬레이터와 Azure 저장소 계정 간에 hello 클라우드에 있습니다. Tooedit hello 연결 문자열 toopoint tooyour 대상 환경을 하기만 하면 됩니다.

Hello를 사용할 수 있습니다 [Microsoft Azure 구성 관리자](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess 응용 프로그램을 실행 하는 위치에 관계 없이 런타임에 연결 문자열입니다.

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>Hello 저장소 에뮬레이터에 대 한 연결 문자열 만들기
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Hello 저장소 에뮬레이터에 대 한 자세한 내용은 참조 [hello Azure 저장소 에뮬레이터를 사용 하 여 개발 및 테스트에 대 한](storage-use-emulator.md)합니다.

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>Azure Storage 계정에 대한 연결 문자열 만들기
toocreate Azure 저장소 계정에 대 한 연결 문자열을 사용 하 여 hello 다음 서식을 지정합니다. HTTP 또는 HTTPS (권장)를 통해 tooconnect toohello 저장소 계정 하려는 여부를 나타내며, 대체 `myAccountName` 저장소 계정 및 바꾸기의 hello 이름의 `myAccountKey` 계정 액세스 키로:

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

예를 들어 연결 문자열은 다음과 유사할 수 있습니다.

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

Azure Storage는 연결 문자열에서 HTTP 및 HTTPS를 모두 지원하지만 *HTTPS를 사용하는 것이 좋습니다.*

> [!TIP]
> Hello에서 저장소 계정의 연결 문자열을 찾을 수 있습니다 [Azure 포털](https://portal.azure.com)합니다. 너무 이동**설정** > **액세스 키** 두 기본 및 보조 액세스 키에 대 한 저장소 계정의 메뉴 블레이드 toosee 연결 문자열에 있습니다.
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>공유 액세스 서명을 사용하여 연결 문자열 만들기
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>명시적 저장소 끝점에 대한 연결 문자열 만들기
Hello 기본 끝점을 사용 하는 대신 연결 문자열에 명시적 서비스 끝점을 지정할 수 있습니다. toocreate 명시적 끝점을 지정 하는 연결 문자열 형식에 따라 hello에서 hello 프로토콜 사양 (HTTPS (권장) 또는 HTTP)를 포함 하 여 각 서비스에 대 한 hello 완전 한 서비스 끝점을 지정 합니다.

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

Toospecify는 명시적 끝점이 사용할 수 있는 한 가지 시나리오는 Blob 저장소 끝점 tooa에 매핑된 경우 [사용자 지정 도메인](storage-custom-domain-name.md)합니다. 이 경우 연결 문자열에 있는 Blob Storage에 대해 사용자 지정 끝점을 지정할 수 있습니다. 필요에 따라 경우 지정할 수 있습니다 hello에 대 한 기본 끝점 hello 다른 서비스를 응용 프로그램에 사용 합니다.

Hello Blob 서비스에 대 한 명시적 끝점을 지정 하는 연결 문자열의 예는 다음과 같습니다.

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

이 예에서는 hello Blob 서비스에 대 한 사용자 지정 도메인을 포함 하는 모든 서비스에 대해 명시적 끝점을 지정 합니다.

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

연결 문자열에 hello 끝점 값은 사용 되는 tooconstruct hello 요청 Uri toohello 저장소 서비스 및 tooyour 코드를 반환 하는 Uri의 hello 형식을 지정 합니다.

저장소 끝점 tooa 사용자 지정 도메인 매핑된 수 toouse 됩니다 한 다음 연결 문자열에서 해당 끝점을 생략 하는 경우 해당 연결 문자열 사용자 코드에서 해당 서비스에 tooaccess 데이터가 있습니다.

> [!IMPORTANT]
> 연결 문자열의 서비스 끝점 값은 `https://`(권장) 또는 `http://`를 포함하는 올바른 형식의 URI여야 합니다. Azure 저장소 HTTPS 사용자 지정 도메인에 아직 지원 하지 않으므로 있습니다 *해야* 지정 `http://` tooa 사용자 지정 도메인을 가리키는 URI는 모든 끝점에 대 한 합니다.
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>끝점 접미사를 사용하여 연결 문자열 만들기
toocreate는 같은 연결 문자열에 지역 또는 서로 다른 끝점 접미사를 사용 하 여 인스턴스 저장소 서비스에 대 한 Azure 중국 또는 Azure 정부, 연결 문자열 형식에 따라 사용 하 여 hello에 대 한 합니다. HTTP 또는 HTTPS (권장)를 통해 tooconnect toohello 저장소 계정 하려는 여부를 나타내며, 대체 `myAccountName` hello 저장소 계정의 이름으로 대체 `myAccountKey` 계정 액세스 키 및 바꾸기 `mySuffix` hello URI로 접미사:

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

다음은 Azure 중국에서 저장소 서비스에 대한 연결 문자열에 대한 예입니다.

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>연결 문자열 구문 분석
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>다음 단계
* [Hello Azure 저장소 에뮬레이터를 사용 하 여 개발 및 테스트](storage-use-emulator.md)
* [Azure Storage 탐색기](storage-explorers.md)
* [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md)

