---
title: "Azure HDInsight에서 Hadoop으로 Twitter 데이터 aaaAnalyze | Microsoft Docs"
description: "Toouse 하이브 tooanalyze Twitter 데이터 Hadoop에서 HDInsight toofind에 특정 단어의 사용 빈도 hello 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>HDInsight에서 Hive를 사용하여 Twitter 데이터 분석
소셜 웹 사이트는 빅 데이터 채택에 대 한 주요 추진 배경과 hello 중 하나입니다. Twitter와 같은 사이트에서 제공하는 공개 API는 대중적인 추세를 분석하고 이해하는 데 유용한 데이터 원본입니다.
이 자습서에서는 스트리밍 API, Twitter를 사용 하 여 트 윗을 가져올 한 다음 Azure HDInsight tooget hello 특정 단어가 포함 된 대부분 윗 보낸 Twitter 사용자의 목록에 Apache Hive를 사용 합니다.

> [!IMPORTANT]
> hello이 문서의 단계는 Windows 기반 HDInsight 클러스터가 필요합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요. 단계 특정 tooa Linux 기반 클러스터에 대 한 참조 [(Linux) HDInsight의 Hive를 사용 하 여 Twitter 분석 데이터](hdinsight-analyze-twitter-data-linux.md)합니다.

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **워크스테이션** .

    tooexecute Windows PowerShell 스크립트를 관리자 권한으로 Azure PowerShell을 실행 하 고 설정 해야 hello 실행 정책을 너무*RemoteSigned*합니다. [Windows PowerShell 스크립트 실행][powershell-script]을 참조하세요.

    Windows PowerShell 스크립트를 실행 하기 전에 hello 다음 cmdlet을 사용 하 여 Azure 구독 연결된 tooyour 있는지를 확인 합니다.

    ```powershell
    Login-AzureRmAccount
    ```

    여러 Azure 구독이 있는 경우 다음 cmdlet tooset hello 현재 구독 하는 hello를 사용 합니다.

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다. Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.
    >
    > Hello 단계에 따라 [설치 Azure PowerShell을 구성 하 고](/powershell/azureps-cmdlets-docs) tooinstall hello 최신 버전의 Azure PowerShell. 해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md) 자세한 정보에 대 한 합니다.

* **Azure HDInsight 클러스터**. 클러스터 프로비전에 대한 자세한 내용은 [HDInsight 사용 시작][hdinsight-get-started] 또는 [HDInsight 클러스터 프로비전][hdinsight-provision]을 참조하세요. Hello 자습서의 뒷부분에 나오는 hello 클러스터 이름이 필요 합니다.

hello 다음 표에이 자습서에 사용 된 hello 파일.

| 파일 | 설명 |
| --- | --- |
| /tutorials/twitter/data/tweets.txt |hello hello 하이브 작업에 대 한 소스 데이터입니다. |
| /tutorials/twitter/output |hello 하이브 작업에 대 한 hello 출력 폴더입니다. hello 기본 하이브 작업 출력 파일 이름은 **000000_0**합니다. |
| tutorials/twitter/twitter.hql |hello HiveQL 스크립트 파일입니다. |
| /tutorials/twitter/jobstatus |Hadoop 작업 상태 번호입니다. |

## <a name="get-twitter-feed"></a>Twitter 피드 가져오기
이 자습서를 사용 하 여 hello [스트리밍 Api Twitter][twitter-streaming-api]합니다. hello 스트리밍 API를 사용 하 여 특정 Twitter은 [상태/필터][twitter-statuses-filter]합니다.

> [!NOTE]
> 공용 Blob 컨테이너에 10, 000 트 윗 및 hello Hive 스크립트 파일 (hello 다음 섹션에 포함 됨)를 포함 하는 파일을 업로드 하지 않았습니다. Toouse hello 업로드 파일을 원하는 경우이 섹션을 건너뛸 수 있습니다.

[트 윗 데이터](https://dev.twitter.com/docs/platform-objects/tweets) 복잡 한 중첩된 구조를 포함 하는 hello 개체 JSON (JavaScript Notation) 형식으로 저장 됩니다. 기존의 프로그래밍 언어를 사용하여 여러 줄의 코드를 작성하는 대신, 이 중첩 구조를 Hive 테이블로 변환하여 HiveQL이라는 SQL(구조적 쿼리 언어)과 유사한 언어로 쿼리할 수 있습니다.

Twitter는 OAuth 권한이 tooprovide 액세스 tooits API를 사용합니다. OAuth에 자신의 암호를 공유 하지 않고 대신 사용자가 tooapprove 응용 프로그램 tooact 수 있는 인증 프로토콜입니다. 자세한 내용은에서 확인할 수 있습니다 [oauth.net](http://oauth.net/) 또는 hello 뛰어난 [초급자 가이드 tooOAuth](http://hueniverse.com/oauth/) Hueniverse에서 합니다.

hello 첫 번째 단계 toouse OAuth toocreate hello Twitter 개발자 사이트에서 새 응용 프로그램입니다.

**toocreate Twitter 응용 프로그램**

1. 역시 로그인[https://apps.twitter.com/](https://apps.twitter.com/)합니다. Hello 클릭 **지금 등록** Twitter 계정이 없는 경우 연결 합니다.
2. **Create New App**을 클릭합니다.
3. **Name**, **Description**, **Website**를 입력합니다. Hello에 대 한 URL을 만들 수 **웹 사이트** 필드입니다. 다음 표에서 hello 몇 가지 샘플 값 toouse를 보여 줍니다.

   | 필드 | 값 |
   | --- | --- |
   |  이름 |MyHDInsightApp |
   |  설명 |MyHDInsightApp |
   |  Website |http://www.myhdinsightapp.com |
4. **Yes, I agree**를 선택한 후 **Create your Twitter application**을 클릭합니다.
5. Hello 클릭 **권한을** 탭 hello 기본 권한은 **읽기 전용**합니다. 이 자습서에는 이 권한이면 충분합니다.
6. Hello 클릭 **키와 액세스 토큰이** 탭 합니다.
7. **Create my access token**을 클릭합니다.
8. 클릭 **테스트 OAuth** hello 페이지의 hello 오른쪽 위 모서리에 있습니다.
9. **consumer key**, **Consumer secret**, **Access token** 및 **Access token secret**을 기록해 둡니다. Hello 자습서의 뒷부분에 나오는 hello 값이 필요 합니다.

이 자습서에서는 Windows PowerShell toomake hello 웹 서비스 호출을 사용 합니다. .NET C# 샘플의 경우 [HDInsight에서 HBase를 사용하여 Twitter 데이터 실시간 분석][hdinsight-hbase-twitter-sentiment]을 참조하세요. hello 다른 인기 있는 도구 toomake 웹 서비스 호출은 [ *Curl*][curl]합니다. Curl은 [여기][curl-download](영문)에서 다운로드할 수 있습니다.

> [!NOTE]
> Hello curl 명령을 사용 하 여 Windows에는 hello 옵션 값에 대 한 단일 따옴표 대신 큰따옴표를 사용 합니다.

**트 윗 tooget**

1. Windows PowerShell 통합 스크립팅 환경 (ISE) hello를 엽니다. (Hello Windows 8 시작 화면에 입력 **PowerShell_ISE** 클릭 하 고 **Windows PowerShell ISE**합니다. [Windows 8 및 Windows에서 Windows PowerShell 시작][powershell-start](영문)을 참조하세요.
2. Hello hello 스크립트 창에 스크립트를 다음을 복사 합니다.

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Hello 스크립트에서 hello 처음 다섯 개의 tooeight 변수를 설정 합니다.

    변수|설명
    ---|---
    $clusterName|Toorun hello 응용 프로그램을 원하는 hello HDInsight 클러스터의 hello 이름입니다.
    $oauth_consumer_key|이 hello Twitter 응용 프로그램 **소비자 키** 앞서 작성 hello Twitter 응용 프로그램을 만들 때.
    $oauth_consumer_secret|이 hello Twitter 응용 프로그램 **소비자 암호** 앞서 작성 합니다.
    $oauth_token|이 hello Twitter 응용 프로그램 **액세스 토큰** 앞서 작성 합니다.
    $oauth_token_secret|이 hello Twitter 응용 프로그램 **액세스 토큰 암호** 앞서 작성 합니다.
    $destBlobName|Hello 출력 blob 이름입니다. hello 기본값은 **tutorials/twitter/data/tweets.txt**합니다. Hello 기본값을 변경 하면 tooupdate hello Windows PowerShell 스크립트를 적절 하 게 해야 합니다.
    $trackString|hello 웹 서비스는 트 윗 관련된 toothese 키워드를 반환 합니다. hello 기본값은 **클라우드, Azure HDInsight**합니다. Hello 기본값을 변경 하면 hello Windows PowerShell 스크립트를 적절 하 게 업데이트 합니다.
    $lineMax|hello 값 개수 트 윗 hello 스크립트는 읽기를 결정 합니다. 트 윗 100 tooread 약 3 분이 필요합니다. 더 큰 숫자를 설정할 수 있지만 더 많은 시간 toodownload 걸립니다.

1. 키를 눌러 **F5** toorun hello 스크립트입니다. 이 문제를 해결 정보를 실행 하는 경우 모든 hello 줄을 선택 하 고 다음 키를 누릅니다 **F8**합니다.
2. 출력이 끝나면 hello의 끝 hello 출력 합니다. 오류 메시지는 빨간색으로 표시됩니다.

유효성 검사 프로시저 hello 출력 파일을 확인할 수 있습니다 **/tutorials/twitter/data/tweets.txt**, Azure 저장소 탐색기 또는 Azure PowerShell을 사용 하 여 Azure Blob 저장소에 있습니다. 파일을 나열하는 샘플 Windows PowerShell 스크립트를 보려면 [HDInsight에서 Blob Storage 사용][hdinsight-storage-powershell]을 참조하세요.

## <a name="create-hiveql-script"></a>HiveQL 스크립트 만들기
Azure PowerShell을 사용 하는 스크립트 파일에 한 번, 패키지 hello HiveQL 문은에 여러 HiveQL 문은 하나 실행할 수 있습니다. 이 자습서에서는 HiveQL 스크립트를 만듭니다. hello 스크립트 파일을 업로드 tooAzure Blob 저장소 이어야 합니다. Hello 다음 섹션에서 Azure PowerShell을 사용 하 여 hello 스크립트 파일을 실행 합니다.

> [!NOTE]
> 공용 Blob 컨테이너에서 hello Hive 스크립트 파일 및 10, 000 트 윗을 포함 하는 파일을 업로드 하지 않았습니다. Toouse hello 업로드 파일을 원하는 경우이 섹션을 건너뛸 수 있습니다.

hello HiveQL 스크립트 hello 다음을 수행 합니다.

1. **Hello tweets_raw 테이블을 삭제** hello 테이블이 이미 존재 하는 경우.
2. **Hello tweets_raw 하이브 테이블 만들기**합니다. 이 임시 하이브 구조화 된 테이블에 대 한 hello 데이터를 더 이상 보유 추출, 변환 및 로드 (ETL) 처리 합니다. 파티션에 대한 자세한 내용은 [Hive 자습서][apache-hive-tutorial](영문)을 참조하세요.
3. **데이터 로드** /tutorials/twitter/data hello 원본 폴더에서. 임시 하이브 테이블 구조에 중첩 된 JSON 형식으로 hello 트 윗 큰 데이터 집합 변환 된 이제 합니다.
4. **Hello 트 윗 테이블 삭제** hello 테이블이 이미 존재 하는 경우.
5. **Hello 트 윗 테이블 만들기**합니다. 하이브를 사용 하 여 hello 트 윗 데이터 집합에 대해 쿼리하려면 먼저 toorun 다른 ETL 프로세스입니다. 이 ETL 프로세스 hello "twitter_raw" 테이블에 저장 된 hello 데이터에 대 한 보다 자세한 테이블 스키마를 정의 합니다.
6. **overwrite 테이블을 삽입**합니다. 이 복잡 한 하이브 스크립트 일정도 긴 MapReduce 작업 집합이 hello Hadoop 클러스터에 의해 합니다. 크기에 따라 데이터 집합 및 hello 클러스터를 약 10 분이 걸릴 수 없습니다.
7. **overwrite 디렉터리 삽입**합니다. 쿼리 및 출력 hello 데이터 집합 tooa 파일을 실행 합니다. 이 쿼리는 "Azure" hello 단어를 포함 하는 대부분 트 윗을 보낼 Twitter 사용자의 목록을 반환 합니다.

**toocreate 하이브 스크립트를 tooAzure 업로드**

1. Windows PowerShell ISE를 엽니다.
2. Hello hello 스크립트 창에 스크립트를 다음을 복사 합니다.

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Hello 스크립트에서 hello 처음 두 개의 변수를 설정 합니다.

   | 변수 | 설명 |
   | --- | --- |
   |  $clusterName |Toorun hello 응용 프로그램을 원하는 hello HDInsight 클러스터 이름을 입력 합니다. |
   |  $subscriptionID |Azure 구독 ID를 입력합니다. |
   |  $sourceDataPath |hello Azure Blob 저장소 위치를 위치 hello 하이브 쿼리 hello 데이터를 읽습니다. 이 변수 toochange을 필요 하지 않습니다. |
   |  $outputPath |hello Azure Blob 저장소 위치 hello 하이브 쿼리 hello 결과 출력 합니다. 이 변수 toochange을 필요 하지 않습니다. |
   |  $hqlScriptFile |hello 위치와 hello HiveQL 스크립트 파일의 hello 파일 이름입니다. 이 변수 toochange을 필요 하지 않습니다. |
4. 키를 눌러 **F5** toorun hello 스크립트입니다. 이 문제를 해결 정보를 실행 하는 경우 모든 hello 줄을 선택 하 고 다음 키를 누릅니다 **F8**합니다.
5. 출력이 끝나면 hello의 끝 hello 출력 합니다. 오류 메시지는 빨간색으로 표시됩니다.

유효성 검사 프로시저 hello 출력 파일을 확인할 수 있습니다 **/tutorials/twitter/twitter.hql**, Azure 저장소 탐색기 또는 Azure PowerShell을 사용 하 여 Azure Blob 저장소에 있습니다. 파일을 나열하는 샘플 Windows PowerShell 스크립트를 보려면 [HDInsight에서 Blob Storage 사용][hdinsight-storage-powershell]을 참조하세요.

## <a name="process-twitter-data-by-using-hive"></a>Hive를 사용하여 Twitter 데이터 처리
모든 hello 준비 작업을 마쳤습니다. 이제 hello 하이브 스크립트를 호출 하 고 hello 결과 확인할 수 있습니다.

### <a name="submit-a-hive-job"></a>Hive 작업 제출
다음 Windows PowerShell 스크립트 toorun hello 하이브 스크립트 hello를 사용 합니다. Tooset hello 첫 번째 변수가 필요 합니다.

> [!NOTE]
> toouse hello 트 윗 및 HiveQL 스크립트 집합 $hqlScriptFile too"/tutorials/twitter/twitter.hql hello 마지막 두 섹션에서 업로드 hello"입니다. toouse hello 된 것을 tooa 공용 blob 업로드, 너무 $hqlScriptFile 설정"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"입니다.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>Hello 결과 확인
다음 Windows PowerShell 스크립트 toocheck hello 하이브 작업 출력 hello를 사용 합니다. Tooset hello 처음 두 개의 변수를 필요 합니다.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> 필드 구분 기호를 hello hello Hive 테이블 \001을 사용 됩니다. hello 구분 기호 hello 출력에 표시 되지 않습니다.

Azure Blob 저장소에 hello 분석 결과 배치한 후 hello 데이터 tooan Azure SQL 데이터베이스/SQL server를 내보낼 파워 쿼리를 사용 하 여 hello 데이터 tooExcel 내보내기 하거나 hello 하이브 ODBC 드라이버를 사용 하 여 응용 프로그램 toohello 데이터 연결 수 있습니다. 자세한 내용은 참조 [HDInsight 사용 하 여 Sqoop][hdinsight-use-sqoop], [HDInsight를 사용 하 여 비행 연착 데이터를 분석][hdinsight-analyze-flight-delay-data], [ 파워 쿼리를 사용 하 여 Excel tooHDInsight 연결][hdinsight-power-query], 및 [Microsoft ODBC Driver 하이브 hello로 Excel 연결 tooHDInsight][hdinsight-hive-odbc]합니다.

## <a name="next-steps"></a>다음 단계
이 자습서에서 살펴본 것 tootransform 구조화 된 Hive 테이블 tooquery에는 구조화 되지 않은 JSON 데이터 집합을 탐색 하 고 Azure에서 HDInsight를 사용 하 여 Twitter에서 데이터를 분석 하는 방법입니다. toolearn 더 참조 하십시오.

* [HDInsight 시작][hdinsight-get-started]
* [HDInsight에서 HBase를 사용하여 Twitter 데이터 실시간 분석][hdinsight-hbase-twitter-sentiment]
* [HDInsight를 사용하여 비행 지연 데이터 분석][hdinsight-analyze-flight-delay-data]
* [파워 쿼리를 사용 하 여 Excel tooHDInsight 연결][hdinsight-power-query]
* [Microsoft ODBC Driver 하이브 hello를 사용 하 여 Excel tooHDInsight 연결][hdinsight-hive-odbc]
* [HDInsight에서 Sqoop 사용][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
