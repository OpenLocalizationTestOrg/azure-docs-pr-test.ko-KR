---
title: "데이터 레이크 저장소 aaaUse hello REST API tooget 시작 | Microsoft Docs"
description: "데이터 레이크 저장소의 tooperform 작업 WebHDFS REST Api를 사용 하 여"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>REST API를 사용하여 Azure Data Lake 저장소 시작
> [!div class="op_single_selector"]
> * [포털](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

이 문서에서는 toouse WebHDFS REST Api와 데이터 레이크 저장소 REST Api tooperform Azure 데이터 레이크 저장소의 파일 시스템 작업 뿐 아니라 관리 계정 하는 방법을 배웁니다. Azure Data Lake 저장소는 계정 관리 작업을 위해 자체 REST API를 제공합니다. 그러나 Data Lake 저장소는 HDFS 및 Hadoop 에코시스템과 호환되기 때문에 파일 시스템 작업에 WebHDFS REST API를 사용하도록 지원합니다.

> [!NOTE]
> 데이터 레이크 저장소에 대 한 REST API 지원 hello에 대 한 자세한 내용은 참조 하십시오. [Azure 데이터 레이크 저장소 REST API 참조](https://msdn.microsoft.com/library/mt693424.aspx)합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure Active Directory 응용 프로그램을 만듭니다**. Azure AD와 hello Azure AD 응용 프로그램 tooauthenticate hello Data Lake 저장소 응용 프로그램을 사용 합니다. 없는 Azure AD와 다양 한 접근 방법 tooauthenticate 않는 **최종 사용자 인증** 또는 **서비스 간 인증**합니다. 지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.
* [cURL](http://curl.haxx.se/). 이 문서에서는 cURL toodemonstrate toomake REST API 데이터 레이크 저장소 계정에 대해 호출 하는 방법입니다.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Azure Active Directory를 사용하여 인증하려면 어떻게 해야 하나요?
Azure Active Directory를 사용 하 여 두 가지 접근 방식을 tooauthenticate를 사용할 수 있습니다.

### <a name="end-user-authentication-interactive"></a>최종 사용자 인증(대화형)
이 시나리오에서는 hello 응용 프로그램에서 사용자 toolog hello를 표시 하 고 모든 hello 작업이 hello 사용자의 hello 컨텍스트에서 수행 됩니다. Hello 대화형 인증에 대 한 단계를 수행 합니다.

1. 응용 프로그램을 통해 hello 사용자 toohello url 리디렉션:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<리디렉션 URI > toobe 인코딩된 URL에서 사용 하기 위해 필요 합니다. 따라서 https://localhost의 경우 `https%3A%2F%2Flocalhost`)를 사용합니다.
   > 
   > 
   
    이 자습서의 hello 용도로 위에 hello URL에서 자리 표시자 값 hello 바꾸고 웹 브라우저의 주소 표시줄에 붙여 넣습니다. Azure 로그인을 사용 하 여 리디렉션된 tooauthenticate 됩니다. 에 성공적으로 로그인 hello 응답이 hello 브라우저의 주소 표시줄에 표시 됩니다. hello 응답 형식에 따라 hello에 포함 됩니다.
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Hello 응답 hello 권한 부여 코드를 캡처하십시오. 이 자습서에서는 hello 인증 코드 hello 웹 브라우저의 주소 표시줄 hello에서에서 복사한 아래와 같이 hello POST 요청 toohello 토큰 끝점에 전달할 수 있습니다.
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > 이 경우 hello \<리디렉션 URI > 인코딩할 수 없는 필요 합니다.
   > 
   > 
3. hello 응답은 액세스 토큰을 포함 하는 JSON 개체 (예: `"access_token": "<ACCESS_TOKEN>"`) 및 새로 고침 토큰 (예: `"refresh_token": "<REFRESH_TOKEN>"`). 응용 프로그램 사용 hello 액세스 토큰 새로 고침 토큰 tooget hello Azure 데이터 레이크 저장소에 액세스할 때 다른 액세스 토큰 액세스 토큰이 만료 된 경우 합니다.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Hello 액세스 토큰이 만료 되 면 아래와 같이 hello 새로 고침 토큰을 사용 하 여 새 액세스 토큰을 요청할 수 있습니다.
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

대화형 사용자 인증에 대한 자세한 내용은 [인증 코드 부여 흐름](https://msdn.microsoft.com/library/azure/dn645542.aspx)을 참조하세요.

### <a name="service-to-service-authentication-non-interactive"></a>서비스 간 인증(비대화형)
이 시나리오에서는 hello hello 응용 프로그램 tooperform hello 작업 자체 자격 증명을 제공합니다. 이 경우 hello 아래와 같은 POST 요청을 실행 해야 합니다. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

이 요청의 hello 출력 권한 부여 토큰에 포함 됩니다 (가리키는 `access-token` hello 출력 아래에)는 REST API 호출으로 전달 이후에 하 합니다. 이 인증 토큰은 이 문서의 뒷부분에서 필요하므로 텍스트 파일에 저장해 두세요.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

이 문서에서는 hello **비 대화형** 접근 방식입니다. 비 대화형 (서비스 간 호출)에 대 한 자세한 내용은 참조 하십시오. [서비스 자격 증명을 사용 하 여 tooservice 호출](https://msdn.microsoft.com/library/azure/dn645543.aspx)합니다.

## <a name="create-a-data-lake-store-account"></a>Data Lake 저장소 계정 만들기
이 작업이 정의 된 hello REST API 호출 기반 [여기](https://msdn.microsoft.com/library/mt694078.aspx)합니다.

다음 cURL 명령을 hello를 사용 합니다. **\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

명령 위에 hello, 바꿉니다 \< `REDACTED` \> hello 권한 부여 토큰으로 앞서 검색 합니다. 이 명령에 대 한 hello 요청 페이로드 hello에 포함 된 **input.json** hello에 대 한 제공 되는 파일 `-d` 위의 매개 변수입니다. hello input.json 파일의 내용을 hello hello 다음과 유사합니다.

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Data Lake 저장소 계정에서 폴더 만들기
이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory)합니다.

다음 cURL 명령을 hello를 사용 합니다. **\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

명령 위에 hello, 바꿉니다 \< `REDACTED` \> hello 권한 부여 토큰으로 앞서 검색 합니다. 이 명령은 라는 디렉터리를 만듭니다. **mytempdir** hello 루트 폴더에 데이터 레이크 저장소 계정입니다.

Hello 작업이 성공적으로 완료 되 면 다음과 같은 응답이 표시 됩니다.

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Data Lake 저장소 계정의 폴더 나열
이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory)합니다.

다음 cURL 명령을 hello를 사용 합니다. **\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

명령 위에 hello, 바꿉니다 \< `REDACTED` \> hello 권한 부여 토큰으로 앞서 검색 합니다.

Hello 작업이 성공적으로 완료 되 면 다음과 같은 응답이 표시 됩니다.

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a>Data Lake 저장소 계정에 데이터 업로드
이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File)합니다.

다음 cURL 명령을 hello를 사용 합니다. **\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

위의 구문 hello에 **-T** 매개 변수는 hello 파일 업로드 하는 hello 위치입니다.

hello 출력은 toohello 다음과 유사 합니다.
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Data Lake 저장소 계정에서 데이터 읽기
이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File)합니다.

Data Lake 저장소 계정에서 데이터를 읽는 작업은 2단계 프로세스입니다.

* 먼저 hello 끝점에 대해 GET 요청을 제출 `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`합니다. 위치 toosubmit hello 다음 GET 요청을 반환 합니다.
* 그런 다음 hello 끝점에 대해 hello GET 요청을 제출 하면 `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`합니다. 이 hello hello 파일 내용의 표시 됩니다.

그러나 차이점이 있기 때문에 hello에 hello 사이의 입력된 매개 변수 먼저 및 hello의 두 번째 단계, hello를 사용할 수 있습니다 `-L` 매개 변수 toosubmit hello에 대 한 첫 번째 요청 합니다. `-L`기본적으로 옵션 위의 두 요청을 결합 하 고 cURL hello 새 위치에 대 한 hello 요청을 다시 실행 하면 됩니다. 마지막으로, hello 출력이 모든 hello 요청 호출이 표시 되며, 같은 다음과 같이 합니다. **\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

출력 유사한 toohello 다음을 나타나야 합니다.

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Data Lake 저장소 계정에서 파일 이름 바꾸기
이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory)합니다.

사용 하 여 hello 다음 toorename 명령 파일을 cURL 합니다. **\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

출력 유사한 toohello 다음을 나타나야 합니다.

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Data Lake 저장소 계정에서 파일 삭제
이 작업이 정의 된 hello WebHDFS REST API 호출 기반 [여기](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory)합니다.

사용 하 여 hello 다음 toodelete 명령 파일을 cURL 합니다. **\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Hello 다음과 같은 출력을 표시 되어야 합니다.

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Data Lake 저장소 계정 삭제
이 작업이 정의 된 hello REST API 호출 기반 [여기](https://msdn.microsoft.com/library/mt694075.aspx)합니다.

사용 하 여 hello 다음을 cURL 명령 toodelete 데이터 레이크 저장소 계정입니다. **\<yourstorename>**을 Data Lake Store 이름으로 바꿉니다.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Hello 다음과 같은 출력을 표시 되어야 합니다.

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>참고 항목
* [Azure Data Lake 저장소와 호환되는 오픈 소스 빅 데이터 응용 프로그램](data-lake-store-compatible-oss-other-applications.md)

