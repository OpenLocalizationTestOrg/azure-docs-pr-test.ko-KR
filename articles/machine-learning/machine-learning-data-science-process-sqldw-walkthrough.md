---
title: "작업에 팀 데이터 과학 프로세스 hello: SQL 데이터 웨어하우스를 사용 하 여 | Microsoft Docs"
description: "활성 중인 고급 분석 프로세스 및 기술"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>작업에 팀 데이터 과학 프로세스 hello: SQL 데이터 웨어하우스를 사용 하 여
이 자습서에서는 진행 구축 및 SQL 데이터 웨어하우스 (SQL DW)를 사용 하 여 기계 학습 모델을 배포 하는 과정-공개적으로 사용할 수 있는 데이터 집합에 대 한 hello [NYC 택시 Trips](http://www.andresmh.com/nyctaxitrips/) 데이터 집합입니다. 여부는 여행에 대 한 팁은 지불 하 고 다중 클래스 분류 및 회귀에 대 한 모델 에서도 설명 지불 hello 팁 금액에 대 한 hello 분포를 예측 하는 생성 된 hello 이진 분류 모델을 예측 합니다.

hello 절차 뒤에 오는 hello [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 워크플로 합니다. 매개 변수를 표시 방법을 toosetup 데이터 과학 환경 tooload SQL DW로 데이터를 hello 하 고 어떻게 SQL DW 또는 IPython 노트북 tooexplore hello 데이터와 엔지니어 기능 toomodel 중 하나를 사용 하는 방법입니다. 그런 다음 표시 방법을 toobuild와 Azure 기계 학습 모델을 배포 합니다.

## <a name="dataset"></a>hello NYC 택시 Trips 데이터 집합
hello NYC 택시 여행 데이터 약 20GB의 압축 된 CSV 파일 (~ 48 GB 압축 되지 않음)로, 기록을 173 백만 개 이상의 개별 라운드트립 및 hello fares 각 시에 대 한 지불 합니다. Hello 픽업 및 자동 전송 위치를 포함 하는 각 여행 레코드 및 익명으로 처리 하는 시간 (드라이버의) 라이선스 번호 해킹 및 hello 메달 (택시의 고유 id) 번호입니다. hello 데이터 hello 2013 년의 모든 왕복에 설명 하 고 각 월에 대 한 두 개의 데이터 집합을 따라 hello에 제공 됩니다.

1. hello **trip_data.csv** 승객, 픽업 지점과 dropoff, 여행 기간 및 여행 길이 수와 같이 여행 세부 정보를 포함 하는 파일입니다. 다음은 몇 가지 샘플 레코드입니다.
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. hello **trip_fare.csv** 파일 hello 요금을 지불 유형, 요금 크기, 추가 요금 및 세금, 팁 및 통행료가, 및 유료 hello 총 금액 등 각 여정에 대해 지불한의 세부 정보를 포함 합니다. 다음은 몇 가지 샘플 레코드입니다.
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

hello **고유 키** toojoin 여행 사용\_데이터와 여행\_요금 hello 세 개의 필드를 다음으로 구성 됩니다.

* medallion,
* hack\_license 및
* pickup\_datetime.

## <a name="mltasks"></a>세 가지 유형의 예측 작업 처리
Hello에 따라 3 개의 예측 문제를 공식화 우리 *팁\_양* tooillustrate 세 종류의 작업을 모델링:

1. **이진 분류**: toopredict 여부 팁 지불 여행, 즉, 한 *팁\_양* 큰 $0 양수 예제 보다는 동안는 *팁\_양* \ 0은 음수 예입니다.
2. **다중 클래스 분류**: toopredict hello 범위 끝의 hello 여행에 대 한 지불 합니다. Hello 나눕니다 *팁\_양* 다섯 개의 bin 또는 클래스에:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **회귀 작업**: toopredict hello 양을 팁은 여행에 대 한 지불 합니다.  

## <a name="setup"></a>고급 분석에 대 한 hello Azure 데이터 과학 환경 설정
Azure 데이터 과학 환 결 tooset 다음이 단계를 수행 합니다.

**고유한 Azure Blob 저장소 계정 만들기**

* 사용자 고유의 Azure blob 저장소를 프로 비전 할 때 또는 최대한 가까운 Azure blob 저장소에 대 한 지리적 위치를 너무 선택**미국 중남부**,이 hello NYC 택시 데이터 저장 됩니다. hello 데이터 hello 공용 blob 저장소 컨테이너 tooa 컨테이너에서 AzCopy를 사용 하 여 고유한 저장소 계정에 복사 됩니다. hello 곧 제공 될 Azure blob 저장소는 tooSouth 중앙 미국, hello 더 빠르게 (4 단계)이이 작업 완료 될 합니다.
* toocreate Azure 저장소 계정, 단계에서 언급 한 내용에 따라 hello [에 대 한 Azure 저장소 계정](../storage/common/storage-create-storage-account.md)합니다. 다음과 같은 저장소 계정 자격 증명에 대 한 hello 값에 대 한 있는지 toomake 메모 될이 연습의 뒷부분에서 필요 합니다.
  
  * **저장소 계정 이름**
  * **저장소 계정 키**
  * **컨테이너 이름을** (하려는 hello 데이터 toobe hello Azure blob 저장소에에서 저장)

**Azure SQL DW 인스턴스를 프로비전합니다.**
hello 설명서에 따라 [SQL 데이터 웨어하우스를 만들](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision SQL 데이터 웨어하우스 인스턴스에 있습니다. Hello 이후 단계에서 사용 되는 SQL 데이터 웨어하우스 자격 증명을 다음에 표기를 사용 하 게 확인 합니다.

* **서버 이름**: <server Name>.database.windows.net
* **SQLDW(데이터베이스) 이름**
* **사용자 이름**
* **암호**

**Visual Studio 및 SQL Server 데이터 도구 설치** 자세한 지침은 [SQL 데이터 웨어하우스에 Visual Studio 2015 및/또는 SSDT(SQL Server Data Tools) 설치](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md)에 요약된 단계를 수행합니다.

**Visual Studio와 함께 Azure SQL DW tooyour를 연결 합니다.** 자세한 내용은 1-2에서 단계를 참조 하십시오. [Visual Studio를 사용 하 여 SQL 데이터 웨어하우스 tooAzure 연결](../sql-data-warehouse/sql-data-warehouse-connect-overview.md)합니다.

> [!NOTE]
> 실행 hello 다음 SQL 데이터 웨어하우스에서 만든 hello 데이터베이스에서 SQL 쿼리 (hello의 3 단계에서 제공 하는 hello 쿼리 대신 항목, 연결) 너무**마스터 키 만들기**합니다.
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**Azure 구독에서 Azure Machine Learning 작업 영역을 만듭니다.** 자세한 지침은 [Azure 기계 학습 작업 영역 만들기](machine-learning-create-workspace.md)에 요약된 단계를 수행합니다.

## <a name="getdata"></a>SQL 데이터 웨어하우스 hello 데이터 로드
Windows PowerShell 명령 콘솔을 엽니다. Hello 다음에 실행할 PowerShell 명령을 toodownload hello 예제 SQL 스크립트 파일을 hello 매개 변수를 사용 하 여 지정한 GitHub tooa 로컬 디렉터리와 공유 म *-DestDir*합니다. Hello 매개 변수 값을 변경할 수 있습니다 *-DestDir* tooany 로컬 디렉터리입니다. 경우 *-DestDir* 존재 하지 않는 hello PowerShell 스크립트에서 생성 됩니다.

> [!NOTE]
> 너무 해야**관리자 권한으로 실행** 경우 PowerShell 스크립트 뒤 hello를 실행할 때 프로그램 *DestDir* 디렉터리 관리자 권한을 toocreate 또는 toowrite tooit 필요 합니다.
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

성공적으로 실행 한 후 현재 작업 디렉터리도 변경*-DestDir*합니다. 있어야 아래와 같은 toosee 화면:

![][19]

사용자 *-DestDir*, hello 다음 관리자 모드에서 PowerShell 스크립트를 실행 합니다.

    ./SQLDW_Data_Import.ps1

Hello PowerShell 스크립트를 실행 하면 hello에 대 한 처음으로 것인지 tooinput hello 정보 Azure SQL DW 및 Azure blob 저장소 계정에서 합니다. 이 PowerShell 스크립트를 완료 하는 경우 처음으로 hello 자격 증명 hello에 대 한 실행 입력 하면 작성 tooa 구성 파일 SQLDW.conf hello 현재 작업 디렉터리에 있습니다. hello이 PowerShell 스크립트 파일의 향후 실행에 hello 옵션 tooread 필요한 모든 매개 변수가이 구성 파일에서. 일부 매개 변수 toochange 해야 할 경우 선택할 수 있습니다 tooinput hello 매개 변수를이 구성 파일을 삭제 하 고 따라 hello 매개 변수 값을 입력 하 여 프롬프트 이나 toochange hello 매개 변수 값에 따라 hello 화면에 hello SQLDW.conf 파일을 편집 하 여 사용자 *-DestDir* 디렉터리입니다.

> [!NOTE]
> Tooavoid 스키마 이름 충돌 hello SQLDW.conf 파일에서 직접 매개 변수를 읽을 때 프로그램 Azure SQL DW에 이미 있는 내용과 주문 하 고, 3 자리 난수는 추가 toohello 스키마 이름은 hello SQLDW.conf 파일에서 hello 기본 스키마 이름으로 각 실행 합니다. PowerShell 스크립트 hello 묻는 메시지를 스키마 이름에 대 한: hello 이름이 사용자 판단에 따라 지정할 수 있습니다.
> 
> 

이 **PowerShell 스크립트** 파일 hello 다음 작업을 완료 합니다.

* AzCopy가 설치되지 않은 경우 **AzCopy 다운로드 및 설치**
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* **데이터 tooyour 개인 blob 저장소 계정에 복사** hello AzCopy 사용 하 여 공용 blob에서
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **Azure SQL DW (LoadDataToSQLDW.sql 실행 중)에서 Polybase tooyour를 사용 하 여 데이터 로드** hello 다음 명령을 사용 하 여 개인 blob 저장소 계정에서 합니다.
  
  * 스키마 만들기
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * 데이터베이스 범위 자격 증명 만들기
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * Azure 저장소 Blob에 대한 외부 데이터 원본 만들기
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * csv 파일에 대한 외부 파일 형식을 만듭니다. 데이터 압축 되며 필드 hello 파이프 문자로 구분 됩니다.
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * Azure Blob 저장소에 NYC Taxi 데이터 집합에 대한 외부 요금 및 여정 테이블을 만듭니다.
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - Azure blob 저장소 tooSQL 데이터 웨어하우스에서에서 외부 테이블에서 데이터 로드

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - 예제 데이터 테이블 (NYCTaxi_Sample)을 만듭니다 하 고 hello 여행 및 요금 테이블에서 SQL 쿼리를 선택 하면에서 tooit 데이터를 삽입 합니다. (이 연습에서는의 몇 가지 단계가 필요 toouse이 예제 테이블입니다.)

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

저장소 계정을 지리적 위치 hello 로드 시간을 영향을 줍니다.

> [!NOTE]
> 개인 blob 저장소 계정의 hello 지리적 위치에 따라 hello 프로세스 공용 blob tooyour 개인 저장소 계정에서 데이터를 복사 수 15 분 정도 걸릴 또는 심지어 더 오래 hello 프로세스 및 저장소 계정에서 데이터 로드 Azure SQL DW tooyour 20 분이 걸릴 수 정도입니다.  
> 
> 

중복 된 소스 및 대상 파일에 있는 경우 수행할 작업 toodecide 해야 합니다.

> [!NOTE]
> 개인 blob 저장소 계정에 이미 hello 공용 blob 저장소 tooyour 개인 blob 저장소 계정에서 복사 하는 hello.csv 파일 toobe 있으면 AzCopy 묻습니다 toooverwrite 삭제할지 해당 합니다. 입력 toooverwrite 원하지  **n**  대화 상자가 나타나면 합니다. Toooverwrite 하려는 경우 **모든** , 입력 **는** 대화 상자가 나타나면 합니다. 입력할 수 있습니다 **y** toooverwrite.csv 파일을 개별적으로 합니다.
> 
> 

![그림 #21][21]

사용자 고유의 데이터를 사용할 수 있습니다. 데이터가 실제 응용 프로그램에서 온-프레미스 컴퓨터에 있으면 AzCopy tooupload 온-프레미스 데이터 tooyour 개인 Azure blob 저장소를 계속 사용할 수 있습니다. Toochange hello 하기만 하면 **소스** 위치 `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, hello hello PowerShell 스크립트 파일 toohello 로컬 디렉터리의 데이터를 포함 하는 AzCopy 명령에에서 있습니다.

> [!TIP]
> 데이터가 실제 응용 프로그램에서 개인 Azure blob 저장소에 이미 있으면 AzCopy hello PowerShell 스크립트 단계 및 hello 데이터 tooAzure SQL DW에 직접 업로드할 hello를 건너뛸 수 있습니다. 여기에 추가 편집 hello 스크립트 tootailor의 데이터 형식 toohello이 필요 합니다.
> 
> 

이 Powershell 스크립트 hello hello 탐색 예제, 데이터 파일, SQLDW_Explorations.sql SQLDW_Explorations.ipynb, SQLDW_Explorations_Scripts.py에 정보를 Azure SQL DW에에서 이러한 세 가지 파일은 즉시 시도 준비 toobe 있도록도 연결 PowerShell 스크립트 hello 완료 합니다.

성공적으로 실행한 후에 다음과 같이 화면에 표시됩니다.

![][20]

## <a name="dbexplore"></a>Azure SQL 데이터 웨어하우스에서 데이터 탐색 및 기능 엔지니어링
이 섹션에서는 **Visual Studio Data Tools**에서 바로 Azure SQL DW에 대해 SQL 쿼리를 실행하여 데이터를 탐색하고 기능을 생성합니다. 명명 된 hello 예제 스크립트에서이 섹션에 사용 되는 모든 SQL 쿼리를 찾을 수 있습니다 *SQLDW_Explorations.sql*합니다. 이 파일은 다운로드 한 tooyour hello PowerShell 스크립트에 의해 로컬 디렉터리를 이미 되었습니다. 또한 [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql)에서 검색할 수 있습니다. 하지만 hello GitHub의 파일에에서 연결 하는 hello Azure SQL DW 정보가 없습니다.

Hello SQL DW 로그인 이름 및 암호와 Visual Studio를 사용 하 여 Azure SQL DW tooyour 연결 하 고 hello 개방 **SQL 개체 탐색기** tooconfirm hello 데이터베이스 및 테이블 가져왔는지 합니다. Hello 검색 *SQLDW_Explorations.sql* 파일입니다.

> [!NOTE]
> tooopen 병렬 데이터 웨어하우스 (PDW) 쿼리 편집기를 사용 하 여 hello **새 쿼리** hello에서 PDW 사용자를 선택 하는 동안 명령을 **SQL 개체 탐색기**합니다. hello 표준 SQL 쿼리 편집기는 PDW에서 지원 되지 않습니다.
> 
> 

Hello 유형의 데이터를 다음은이 섹션에서 탐색 및 기능 생성 작업 수행:

* 다양한 기간에 걸쳐 몇몇 필드의 데이터 분포를 탐색합니다.
* Hello 경도 및 위도 필드의 데이터 품질을 조사 합니다.
* 이진 및 다중 클래스 분류 레이블을 hello에 따라 생성 **팁\_양**합니다.
* 기능을 생성하고 여정 거리를 계산/비교합니다.
* Hello 두 테이블을 조인 하 고 사용 하는 toobuild 모델 될 무작위 샘플링을 추출 합니다.

### <a name="data-import-verification"></a>데이터 가져오기 확인
이러한 쿼리는 hello hello 이전 Polybase의 병렬 대량을 사용 하 여 채울 테이블 가져오기의 행과 열 수를 빠르게 확인할을 제공 합니다.

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**출력:** 173,179,759행과 14개의 열이 표시됩니다.

### <a name="exploration-trip-distribution-by-medallion"></a>탐색: medallion별 여정 분포
다음 쿼리 예에서는 지정된 된 기간 내에서 100 개 이상의 왕복을 완료 하는 hello medallions (택시 번호)을 식별 합니다. hello 쿼리는 것이 유리한 hello 분할 된 테이블 액세스에서의 파티션 구성표 hello 전제로 이후 **픽업\_datetime**합니다. Hello 전체 데이터 집합 쿼리 hello 분할 된 테이블의 사용 및/또는 색인 검색 또한 확인 됩니다.

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**출력:** hello 쿼리 hello 13,369 medallions (택시)를 지정 하는 행이 있는 테이블을 반환 해야 및 hello 여행 2013에서 타인이 완료 수입니다. hello 마지막 열 완료와의 hello 횟수 hello 수를 포함 합니다.

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>탐색: medallion 및 hack_license별 여정 분포
이 예에서는 hello medallions (택시 번호)을 식별 하 고 hack_license 번호 (드라이버) 완료 하는 두 개 이상의 100와 지정된 된 기간 내에서 키를 누릅니다.

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**출력:** hello 쿼리가 hello 13,369 자동차/드라이버에서에서 완료 된 더 해당 100 trips 2013 Id를 지정 하는 13,369 행이 있는 테이블을 반환 해야 합니다. hello 마지막 열 완료와의 hello 횟수 hello 수를 포함 합니다.

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>데이터 품질 평가: 경도 및/또는 위도가 잘못된 레코드 확인
이 예제에서는 조사 경우 잘못 된 값을 포함 하거나 hello 위도 및 경도 필드 (라디안 각도-90에서 90 사이의 이어야 함), 수도 있고 (0, 0) 좌표입니다.

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**출력:** hello 쿼리에서 잘못 된 경도 및 위도 필드가 있는 837,467 trips 반환 합니다.

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>탐색: 왕복 여정과 비왕복 여정 분포
이 예제에서는 지정된 된 기간 (또는 hello 전체 데이터 집합에서 다음 설정으로 hello 정식 연도 포함 하는 경우) 크리스마스 되지 않은 하는 hello 번호 및 크리스마스 된와의 hello 수를 찾습니다. 이 배포는 나중에 이진 분류 모델링에 사용 하는 hello 이진 레이블 배포 toobe를 반영 합니다.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**출력:** 해야 반환 hello 다음 팁 주파수 2013: 90,447,622 크리스마스 hello 년과 not 위의 82,264,709 쿼리 hello 합니다.

### <a name="exploration-tip-classrange-distribution"></a>탐색: 팁 클래스/범위 분포
이 예에서는 기간에 (또는 hello 전체 데이터 집합의 hello 연도 포함 하는 경우) 주어진된 시간에 팁 범위의 hello 분포를 계산 합니다. 다중 클래스 분류 모델링에 나중에 사용 하는 hello 레이블 클래스의 hello 분포입니다.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

**출력:**

| tip_class | tip_freq |
| --- | --- |
| 1 |82230915 |
| 2 |6198803 |
| 3 |1932223 |
| 0 |82264625 |
| 4 |85765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>탐색: 여정 거리 계산 및 비교
이 예제에서는 hello 픽업 및 자동 전송 경도 변환한 위도 tooSQL geography 가리키는 SQL geography 포인트 차이 사용 하 여 hello 여행 거리를 계산 하 고 비교에 대 한 hello 결과의 무작위 샘플링을 반환 합니다. hello 예제 toovalid만 앞에서 설명 하는 hello 데이터 품질 평가 쿼리를 사용 하 여 조정 하는 hello 결과 제한 합니다.

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a>SQL 함수를 사용하는 기능 엔지니어링
때때로 SQL 함수는 기능 엔지니어링에 대한 효율적인 옵션일 수 있습니다. 이 연습에서는 SQL 함수 toocalculate hello 직접 사이 거리를 hello 픽업 및 dropoff 위치를 정의 했습니다. Hello 뒤에 SQL 스크립트를 실행할 수 있습니다 **Visual Studio 데이터 도구**합니다.

다음은 hello 거리 함수를 정의 하는 hello SQL 스크립트입니다.

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

다음은 예제 toocall 함수 toogenerate 기능이 SQL 쿼리:

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**출력:** 픽업 및 dropoff latitude 된 (행이 있는 테이블 2,803,538)를 생성 하는이 쿼리 및 위 도와 경도 및 hello 해당 직접 마일 거리입니다. 처음 3 행에 대 한 hello 결과 다음과 같습니다.

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40.731804 |-74.001083 |40.736622 |-73.988953 |.7169601222 |
| 2 |40.715794 |-74,010635 |40.725338 |-74.00399 |.7448343721 |
| 3 |40.761456 |-73.999886 |40.766544 |-73.988228 |0.7037227967 |

### <a name="prepare-data-for-model-building"></a>모델 구축에 사용할 데이터를 준비합니다.
hello 다음 쿼리는 조인 hello **nyctaxi\_여행** 및 **nyctaxi\_요금** 테이블, 이진 분류 레이블이 생성 **크리스마스**, 즉 다중 클래스 분류 레이블을 **팁\_클래스**, hello 전체 조인 된 데이터 집합에서 샘플을 추출 합니다. hello 샘플링 픽업 시간을 기반으로 하는 hello와 하위 집합을 검색 하면 됩니다.  이 쿼리를 복사 후 hello에 직접 붙여넣을 수 [Azure 기계 학습 스튜디오](https://studio.azureml.net) [데이터 가져오기] [ import-data] hello SQL 데이터베이스 인스턴스에서 직접 데이터 수집에 대 한 모듈 azure입니다. 잘못 된 레코드를 제외 하는 hello 쿼리 (0, 0) 좌표입니다.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

준비 tooproceed tooAzure 기계 학습을 있습니다 수 있습니다.  

1. Hello 최종 SQL 쿼리 tooextract 및 샘플 hello 데이터 및 복사-붙여넣기 hello에 직접 쿼리를 저장 한 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈 또는
2. 샘플링 hello 유지 및 toouse 건물 새 SQL DW에는 모델에 대 한 계획 엔지니어링된 데이터 테이블 및 hello 새 테이블을 사용 하 여 hello에 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈입니다. hello 이전 단계에서 PowerShell 스크립트를 클릭할 때 수행이 있습니다. Hello 데이터 가져오기 모듈에서이 테이블에서 직접 읽을 수 있습니다.

## <a name="ipnb"></a>IPython Notebook에서 데이터 탐색 및 기능 엔지니어링
이 섹션에서는 데이터 탐색 및 두 Python을 사용 하는 기능 세대를 수행 합니다 하 고 앞에서 만든 SQL DW hello에 대 한 SQL 쿼리 합니다. 명명 된 샘플 IPython 노트북 **SQLDW_Explorations.ipynb** 및 Python 스크립트 파일 **SQLDW_Explorations_Scripts.py** 로컬 디렉터리에 다운로드 한 tooyour 되었습니다. 또한 [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW)에서 사용할 수 있습니다. 이 두 파일은 Python 스크립트에서 동일합니다. hello Python 스크립트 파일은 IPython 노트북 서버가 존재 하지 않는 경우 tooyou를 제공 됩니다. 이 두 샘플 Python 파일은 **Python 2.7**에서 디자인됩니다.

hello 샘플 IPython 노트북에에서 필요한 Azure SQL DW 정보 hello 및 스크립트 파일 다운로드 한 tooyour 로컬 컴퓨터에 전원이 연결 된 hello PowerShell 스크립트에서 이전에 Python hello 합니다. 수정 없이 실행할 수 있습니다.

AzureML 작업 영역을 이미 설정한 경우 직접 업로드 hello 샘플 IPython 노트북 toohello AzureML IPython 노트북 서비스 및 실행을 시작 합니다. Hello 단계 tooupload tooAzureML IPython 노트북 서비스는 다음과 같습니다.

1. tooyour AzureML 작업 영역, "Studio" hello 위쪽에 클릭 하 고 hello hello 웹 페이지의 왼쪽에 "노트북"를 클릭 합니다.
   
    ![그림 #22][22]
2. Hello 웹 페이지의 왼쪽된 아래 모서리 hello에 "NEW"를 클릭 하 고 선택 "Python 2" 입니다. 그런 다음, 이름 toohello 노트북을 제공 하 고 hello 확인 표시가 toocreate hello 새 빈 IPython 노트북을 클릭 합니다.
   
    ![그림 #23][23]
3. Hello hello의 왼쪽된 위 모서리에 hello "Jupyter" 기호를 클릭 합니다. 새 IPython 전자 필기장 합니다.
   
    ![그림 #24][24]
4. 끌어서 놓기 샘플 IPython 노트북 toohello hello **트리** AzureML IPython 노트북 서비스의 페이지로 **업로드**합니다. 그러면 hello 샘플 IPython 노트북 업로드 toohello AzureML IPython 노트북 서비스 됩니다.
   
    ![그림 #25][25]

순서 toorun hello 예제 IPython 노트북 또는 Python 스크립트 파일을 hello, hello 다음 Python 패키지가 필요 합니다. Hello AzureML IPython 노트북 서비스를 사용 하는 경우 이러한 패키지가 미리 설치 되었습니다.

    - pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

대규모 데이터 AzureML에 고급 분석 솔루션을 빌드할 때 순서를 권장 하는 hello는 hello 다음:

* 메모리 내 데이터 프레임으로 hello 데이터의 작은 샘플에서 읽어옵니다.
* 일부 시각화 및 탐색 하는 hello 샘플링 된 데이터를 사용 하 여 수행 합니다.
* 데이터를 샘플링 하는 hello를 사용 하 여 기능 엔지니어링 놓습니다.
* 더 큰 데이터 탐색에 대 한 데이터 조작 및 기능 엔지니어링 hello SQL DW에 대 한 직접 Python tooissue SQL 쿼리를 사용 합니다.
* Azure 기계 학습 모델 작성에 대 한 적합 한 hello 샘플 크기 toobe를 결정 합니다.

hello 사항은 몇 가지 데이터 탐색, 데이터 시각화 및 기능 엔지니어링 예제입니다. Hello 샘플 IPython 전자 필기장 및 hello 샘플 Python 스크립트 파일에 더 많은 데이터 탐색을 찾을 수 있습니다.

### <a name="initialize-database-credentials"></a>데이터베이스 자격 증명 초기화
데이터베이스 연결 설정에서 다음 변수는 hello 초기화 합니다.

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>데이터베이스 연결 만들기
다음은 hello 연결 toohello 데이터베이스를 만드는 hello 연결 문자열입니다.

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><nyctaxi_trip> 테이블의 행 및 열 수 보고
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* 총 행 수 = 173179759  
* 총 열 수 = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><nyctaxi_fare> 테이블의 행 및 열 수 보고
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* 총 행 수 = 173179759  
* 총 열 수 = 11

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>읽기에 hello SQL 데이터 웨어하우스 데이터베이스에서에서 작은 데이터 샘플
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

시간 tooread hello 예제 테이블은 14.096495 초입니다.  
검색된 행 및 열 수 = (1000, 21)

### <a name="descriptive-statistics"></a>기술 통계
이제는 준비 tooexplore hello 샘플링 된 데이터입니다. Hello에 대 한 기술 통계를 살펴보면 가장 먼저 **여행\_거리** (또는 toospecify 선택할 다른 필드).

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>시각화: 상자 그림 예제
다음 hello 여행 거리 toovisualize hello 변 위치에 대 한 hello 상자 그림을 살펴보겠습니다.

    df1.boxplot(column='trip_distance',return_type='dict')

![그릴 #1][1]

### <a name="visualization-distribution-plot-example"></a>시각화: 분포 그림 예제
여행 거리를 샘플링 하는 hello 배포 및 hello에 대 한 히스토그램을 시각화 하는 점도.

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![그릴 #2][2]

### <a name="visualization-bar-and-line-plots"></a>시각화: 가로 막대형 차트 및 꺾은선형 그림
이 예제에서는 hello 여행 거리 다섯 개의 bin으로 범주화 하 고 결과 범주화 하는 hello를 시각화 합니다.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Bin 분포 막대에서 위에 hello 그릴 하거나 플롯을 줄 수 있습니다.:

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![그릴 #3][3]

and

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![그릴 #4][4]

### <a name="visualization-scatterplot-examples"></a>시각화: 산점도 예제
산 점도 간에 매개 변수를 표시 **여행\_시간\_에\_초** 및 **여행\_거리** toosee 상관 관계 없는 경우

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![그릴 #6][6]

Hello 관계 확인할 수 있습니다 마찬가지로 **속도\_코드** 및 **여행\_거리**합니다.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![그릴 #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>IPython Notebook에서 SQL 쿼리를 사용하여 샘플링된 데이터에서 데이터 탐색
이 섹션에서는 위에서 만든 hello 새 테이블에서 유지 되는 hello 샘플링 된 데이터를 사용 하 여 데이터 분포 탐색 합니다. 참고 비슷한 탐색 hello 원래 테이블을 사용 하 여 수행할 수 있도록 합니다.

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>탐색: 샘플링 된 테이블의 행과 열 hello의 보고서 수
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>탐색: 왕복/비왕복 분포
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>탐색: 팁 클래스 분포
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>탐색: 클래스에 의해 hello 팁 배포 그림
    tip_class_dist['tip_freq'].plot(kind='bar')

![그림 #26][26]

#### <a name="exploration-daily-distribution-of-trips"></a>탐색: 일일 여정 분포
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>탐색: medallion당 여정 분포
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>탐색: medallion 및 hack license별 여정 분포
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>탐색: 여정 시간 분포
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>탐색: 여정 거리 분포
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>탐색: 지불 형식 분포
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Hello hello 들어가지 않고 기능화 테이블의 최종 형태를 확인 합니다.
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a>Azure 기계 학습에서 모델 빌드
준비 tooproceed toomodel 건물과 모델 배포에는 이제 [Azure 기계 학습](https://studio.azureml.net)합니다. hello 데이터는 hello 예측 문제 즉 앞에서 확인에 사용 되는 준비 toobe입니다.

1. **이진 분류**: toopredict 트립이 팁 지불 여부.
2. **다중 클래스 분류**: toohello 이전에 정의 된 클래스에 따라 지불을 끝의 toopredict hello 범위입니다.
3. **회귀 작업**: toopredict hello 양을 팁은 여행에 대 한 지불 합니다.  

toobegin 모델링 훈련 hello, tooyour 로그인 **Azure 기계 학습** 작업 영역입니다. 기계 학습 작업 영역을 아직 만들지 않은 경우 [Azure 기계 학습 작업 영역 만들기](machine-learning-create-workspace.md)를 참조하세요.

1. Azure 기계 학습 시작 tooget 참조 [Azure 기계 학습 스튜디오는 무엇입니까?](machine-learning-what-is-ml-studio.md)
2. 로그 너무[Azure 기계 학습 스튜디오](https://studio.azureml.net)합니다.
3. hello Studio 홈 페이지는 다양 한 정보, 비디오, 자습서, 링크 toohello 모듈 참조 및 기타 리소스를 제공합니다. Azure 기계 학습에 대 한 자세한 내용은 참조 hello [Azure 기계 학습 설명서 센터](https://azure.microsoft.com/documentation/services/machine-learning/)합니다.

일반적인 학습 실험 단계를 수행 하는 hello 이루어져 있습니다.

1. **+새** 실험 만들기
2. Azure 기계 학습에 hello 데이터를 가져옵니다.
3. 전처리 하 고, 변환 및 필요에 따라 hello 데이터를 조작 합니다.
4. 필요에 따라 기능을 생성합니다.
5. Hello 데이터를 학습 /, 유효성 검사, 테스트 데이터 집합 분할 (별도 데이터 집합 수도 있고 각각에 대해).
6. 하나 이상의 기계 학습 문제 toosolve 학습 hello에 따라 알고리즘을 선택 합니다. 이진 분류, 다중 클래스 분류, 회귀)을 선택합니다.
7. Hello 학습 데이터 집합을 사용 하 여 하나 이상의 모델을 학습 합니다.
8. Hello 학습 된 모델을 사용 하 여 hello 유효성 검사 데이터 집합을 점수를 매깁니다.
9. Hello 모델로 toocompute hello 관련 메트릭 hello 학습 문제에 대 한 평가 합니다.
10. Hello 모델 및 선택 hello 최상의 모델 toodeploy 미세 조정 합니다.

이 연습에서는 이미 탐색 및 SQL 데이터 웨어하우스에 데이터가 보존 hello 엔지니어링 했으며 hello 샘플 크기 tooingest Azure 기계 학습에서 결정 합니다. 하나 이상의 hello 예측 모델 hello 프로시저 toobuild 다음과 같습니다.

1. Hello 데이터 hello를 사용 하 여 Azure ML로 가져오므로 [데이터 가져오기] [ import-data] hello에서 사용할 수 있는 모듈 **데이터 입력 및 출력** 섹션. 자세한 내용은 참조 hello [데이터 가져오기] [ import-data] 모듈 참조 페이지입니다.
   
    ![Azure ML 데이터 가져오기][17]
2. 선택 **Azure SQL 데이터베이스** hello로 **데이터 소스** hello에 **속성** 패널입니다.
3. Hello에 hello 데이터베이스 DNS 이름을 입력 **데이터베이스 서버 이름** 필드입니다. 형식: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Hello 입력 **데이터베이스 이름** hello 해당 필드에 있습니다.
5. Hello 입력 *SQL 사용자 이름* hello에 **서버 사용자 계정 이름**, 및 hello *암호* hello에 **서버 사용자 계정 암호**합니다.
6. Hello 확인 **모든 서버 인증서 수락** 옵션입니다.
7. Hello에 **데이터베이스 쿼리** 텍스트 영역을 편집, hello 필요한 데이터베이스 필드 (예: hello 레이블 모든 계산된 필드 포함), 아래에 추출 hello 데이터 원하는 toohello 샘플 크기를 샘플링 하는 hello 쿼리를 붙여 넣습니다.

Hello SQL 데이터 웨어하우스 데이터베이스에서 직접 데이터를 읽는 이진 분류 실험 실제 예는 아래 hello 그림 (기억 tooreplace hello 테이블 이름은 nyctaxi_trip 및 nyctaxi_fare hello 스키마에서 이름과 hello 테이블 이름에 사용한 사용자 연습)입니다. 다중 클래스 분류 및 회귀 문제에 대한 유사한 실험을 생성할 수 있습니다.

![Azure 기계 학습][10]

> [!IMPORTANT]
> 데이터 추출을 모델링 하 고 이전 섹션에서 제공 하는 쿼리 예제 샘플링 hello에 **hello 3 모델링 연습에 대 한 모든 레이블을 hello 쿼리에 포함 된**합니다. 각 연습을 모델링 하는 hello (필수) 중요 한 단계는 너무**제외** 다른 두 가지 문제 및 기타 hello에 대 한 불필요 한 레이블을 hello **누수 대상**합니다. 이진 분류를 사용할 때는 hello 레이블을 사용 하 여 예를 들어 **크리스마스** hello 필드를 제외 하 고 **팁\_클래스**, **팁\_양**, 및 **총\_양**합니다. 후자의 hello 대상 누수 hello 팁 사실도 지불 됩니다.
> 
> tooexclude 모든 불필요 한 열 또는 대상, 즉 누수를 hello를 사용할 수 있습니다 [데이터 집합의 열 선택] [ select-columns] 모듈 또는 hello [메타 데이터 편집] [ edit-metadata]. 자세한 내용은 [데이터 집합의 열 선택][select-columns] 및 [메타데이터 편집][edit-metadata] 참조 페이지를 참조하세요.
> 
> 

## <a name="mldeploy"></a>Azure 기계 학습에서 모델 배포
모델에 준비 되 면 hello 실험에서 직접 웹 서비스로 쉽게 배포할 수 있습니다. Azure 기계 학습 웹 서비스 배포에 대한 자세한 내용은 [Azure 기계 학습 웹 서비스 배포](machine-learning-publish-a-machine-learning-web-service.md)를 참조하세요.

새 웹 서비스 toodeploy 해야합니다.

1. 점수 매기기 실험을 만듭니다.
2. Hello 웹 서비스를 배포 합니다.

점수 매기기를 실험 toocreate는 **마침** 클릭 실험 교육, **점수 매기기 실험 만들기** hello 아래 작업 표시줄에 합니다.

![Azure 점수 매기기][18]

Azure 기계 학습 점수 매기기 실험 hello 학습 실험의 hello 구성 요소에 따라 toocreate를 시도 합니다. 특히 다음 작업을 수행합니다.

1. Hello 학습 된 모델을 저장 하 고 hello 모델 학습 모듈을 제거 합니다.
2. 논리적 식별 **입력 포트** toorepresent hello 입력된 데이터 스키마를 예상 합니다.
3. 논리적 식별 **출력 포트** toorepresent hello 예상된 웹 서비스 출력 스키마입니다.

Hello 실험 점수 매기기를 만들면 검토 하 고 필요에 따라 조정 확인 합니다. 이러한 표시 되지 것입니다 hello 서비스를 호출 하는 경우 일반적인 조정은 tooreplace hello 입력된 데이터 집합 및/또는 레이블 필드를 제외를 사용 하 여 쿼리 합니다. 것이 좋습니다 tooreduce hello 크기인 hello 입력 데이터 집합 및/또는 쿼리 tooa 소수의 레코드 데 충분 한 tooindicate hello 입력된 스키마도입니다. Hello 출력 포트에 대 한 일반적인 tooexclude 모든 입력된 필드 이며 hello 포함 **점수가 매겨진 레이블** 및 **점수가 매겨진 확률** hello hello를 사용 하 여 출력에 [데이터 집합의 열 선택 ] [ select-columns] 모듈입니다.

샘플 실험을 점수 매기기 아래 hello 그림에서 제공 됩니다. Toodeploy, 준비 되 면 hello 클릭 **웹 서비스 게시** hello 낮은 작업 모음에서 단추입니다.

![Azure ML 게시][11]

## <a name="summary"></a>요약
toorecap이 연습에서는 자습서에 맞게 했던 만든에 큰 공용 데이터 집합으로 작업 하는 Azure 데이터 과학 환경 hello 데이터 취득 toomodel 학습에서 모든 hello 방법 팀 데이터 과학 프로세스를 통해 작성 한 다음 Azure 기계 학습 웹 서비스의 toohello 배포 합니다.

### <a name="license-information"></a>라이선스 정보
이 샘플 연습 및 그에 따른 스크립트 및 IPython notebook(s)은 hello MIT 라이선스에 따라 Microsoft에서 공유 됩니다. 자세한 내용은 GitHub에서 hello 샘플 코드의 hello 디렉터리에 hello LICENSE.txt 파일 확인 하십시오.

## <a name="references"></a>참조
• [Andrés Monroy NYC Taxi Trips 다운로드 페이지](http://www.andresmh.com/nyctaxitrips/)  
• [Chris Whong의 FOILing NYC Taxi Trip 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC Taxi 및 Limousine 수수료 연구 및 통계](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
