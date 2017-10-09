---
title: "aaaBuild Azure VM에서 SQL Server를 사용 하 여 기계 학습 모델을 배포 하 고 | Microsoft Docs"
description: "활성 중인 고급 분석 프로세스 및 기술"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>작업에 팀 데이터 과학 프로세스 hello: SQL Server를 사용 하 여
Hello 만들고 기계 학습 모델을 배포 하는 과정을 단계별로 안내이 자습서에서는 사용 하 여 SQL Server 및 공개적으로 사용할 수 있는 데이터 집합-hello [NYC 택시 Trips](http://www.andresmh.com/nyctaxitrips/) 데이터 집합입니다. hello 프로시저 표준 데이터 과학 워크플로 따릅니다: 수집 하 고 hello 데이터 탐색, 엔지니어링 기능 toofacilitate 학습 한 다음 빌드 및 모델을 배포 합니다.

## <a name="dataset"></a>NYC Taxi Trips 데이터 집합 설명
hello NYC 택시 여행 데이터는 약 20GB의 압축 된 CSV 파일 (~ 48 GB 압축 되지 않음), 구성 173 백만 개 이상의 개별 라운드트립 및 hello fares 각 시에 대 한 지불 합니다. 각 여행 레코드 hello 픽업 및 자동 전송 위치 및 시간, 익명화 된 해킹 (드라이버의) 라이선스 번호 및 메달 (택시의 고유 id) 번호를 포함합니다. hello 데이터 hello 2013 년의 모든 왕복에 설명 하 고 각 월에 대 한 두 개의 데이터 집합을 따라 hello에 제공 됩니다.

1. hello 'trip_data' CSV 승객, 픽업 및 dropoff 포인트, 여행 기간 및 여행 길이 수와 같이 여행 세부 정보를 포함합니다. 다음은 몇 가지 샘플 레코드입니다.
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. hello 'trip_fare' CSV hello 요금을 지불 유형, 요금 크기, 추가 요금 및 세금, 팁 및 통행료가, 및 유료 hello 총 금액 등 각 여정에 대해 지불한의 세부 정보를 포함 합니다. 다음은 몇 가지 샘플 레코드입니다.
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

hello 고유 키 toojoin 여행\_데이터와 여행\_요금 가지 hello 필드로 구성 됩니다: 메달 해킹\_사용권 및 픽업\_날짜/시간입니다.

## <a name="mltasks"></a>예측 작업의 예제
우리는 hello에 따라 3 개의 예측 문제 작성 *팁\_양*, 즉:

1. 이진 분류: 여정에 대해 팁이 지불되었는지 여부를 예측합니다. 즉, *tip\_amount*가 $0보다 크면 지불된 것이고 *tip\_amount*가 $0이면 지불되지 않은 것입니다.
2. 다중 클래스 분류: toopredict hello 범위 끝의 hello 여행에 대 한 지불 합니다. Hello 나눕니다 *팁\_양* 다섯 개의 bin 또는 클래스에:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. 회귀 작업: toopredict hello 양을 팁은 여행에 대 한 지불 합니다.  

## <a name="setup"></a>설정 hello Azure 데이터 과학 환경에 대 한 고급 분석
Hello에서 볼 수 있듯이 [환경 계획](machine-learning-data-science-plan-your-environment.md) 가이드는 Azure의 hello NYC 택시 Trips 데이터 집합이 들어 있는 몇 가지 옵션 toowork:

* Azure blob에 hello 데이터 다음 Azure 기계 학습에서 모델 사용
* Hello 데이터를 SQL Server 데이터베이스 다음 Azure 기계 학습에서 모델 로드

이 자습서에서는 SQL Server, 데이터 탐색, 기능 hello 데이터 tooa의 병렬 대량 가져오기를 보여 드리겠습니다 엔지니어링 및 SQL Server Management Studio를 사용 하 여 샘플링 아래쪽으로 IPython 노트북을 사용 하 여 합니다. [샘플 스크립트](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) 및 [IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)은 GitHub에서 공유됩니다. Azure blob에 대 한 hello 데이터로 샘플 IPython 노트북 toowork hello 제공 됩니다. 동일한 위치입니다.

Azure 데이터 과학 환 결 tooset:

1. [저장소 계정을 만드는](../storage/common/storage-create-storage-account.md)
2. [Azure 기계 학습 작업 영역 만들기](machine-learning-create-workspace.md)
3. [데이터 과학 가상 컴퓨터 프로비전](machine-learning-data-science-setup-sql-server-virtual-machine.md)(SQL Server 및 IPython Notebook 서버 제공)
   
   > [!NOTE]
   > hello 예제 스크립트 및 IPython 노트북이 다운로드 한 tooyour 데이터 과학 가상 컴퓨터 hello 설치 프로세스 중 됩니다. Hello VM 설치 후 스크립트에는 다음이 완료 되 면 hello 샘플 VM의 문서 라이브러리에서 됩니다.  
   > 
   > * 샘플 스크립트: `C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * 샘플 IPython Notebook: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   where `<user_name>` 은(는) VM의 Windows 로그인 이름입니다. Toohello 예제 폴더를 언급할 **예제 스크립트** 및 **샘플 IPython 노트북**합니다.
   > 
   > 

Hello 데이터 집합의 크기, 데이터 원본 위치 및 hello 선택한 Azure 대상 환경에 따라,이 시나리오는 비슷한 너무[시나리오 \#5: 로컬 파일에 큰 데이터 집합에는 Azure VM의 SQL Server 대상](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb)합니다.

## <a name="getdata"></a>공개 소스에서 hello 데이터 가져오기
tooget hello [NYC 택시 Trips](http://www.andresmh.com/nyctaxitrips/) 공용 위치에서 데이터 집합을 사용할 수 있습니다에 설명 된 hello 메서드의 [Azure Blob 저장소에서 데이터 이동 tooand](machine-learning-data-science-move-azure-blob.md) toocopy hello 데이터 tooyour 새 가상 컴퓨터.

AzCopy를 사용 하 여 toocopy hello 데이터:

1. Tooyour 가상 컴퓨터 (VM)에 로그인
2. Hello VM 데이터 디스크에 새 디렉터리를 만듭니다 (참고: hello 데이터 디스크로 VM hello와 함께 제공 되는 임시 디스크를 사용 하지 않습니다).
3. 명령 프롬프트 창에서 다음 Azcopy 명령 줄, (2)에서 만든 데이터 폴더와 < path_to_data_folder > 대체 hello를 실행 합니다.
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    총 24 CSV 파일을 압축 hello AzCopy 완료 되 면 (여행에 대 한 12\_데이터와 여행에 대 한 12\_요금) hello 데이터 폴더에 있어야 합니다.
4. Hello 다운로드 한 파일을 압축을 풉니다. 참고 hello 폴더 hello 압축 되지 않은 파일이 있는입니다. 이 폴더에는 참조 된 tooas hello 됩니다 < 경로\_를\_데이터\_파일\>합니다.

## <a name="dbload"></a>SQL Server 데이터베이스로 대량 데이터 가져오기
hello 로드/전송 많은 양의 데이터 tooan SQL 데이터베이스 및 후속 쿼리 성능이 향상 될 수 있습니다를 사용 하 여 *분할 테이블 및 뷰*합니다. 이 섹션에 설명 된 hello 지침을 따릅니다 [병렬 대량 데이터 가져오기를 사용 하 여 SQL 파티션 테이블](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate를 동시에 분할 된 테이블에 새 데이터베이스 및 부하 hello 데이터입니다.

1. Tooyour VM에에서 로그인 한 상태, 시작 **SQL Server Management Studio**합니다.
2. Windows 인증을 사용하여 연결
   
    ![SSMS 연결][12]
3. Hello SQL Server 인증 모드를 변경 하지 않은 있고 새 SQL 로그인 사용자를 만든 경우 hello 스크립트 파일을 열고 **변경\_auth.sql** hello에 **예제 스크립트** 폴더입니다. Hello 기본 사용자 이름과 암호를 변경 합니다. 클릭 **! 실행** hello 도구 모음 toorun hello 스크립트에 있습니다.
   
    ![스크립트 실행][13]
4. 확인 및/또는 변경 hello SQL Server를 새로 만든 데이터베이스는 기본 데이터베이스 및 로그 폴더 tooensure 데이터 디스크에 저장 됩니다. 데이터 웨어하우징 로드에 대해 최적화 된 hello SQL Server VM 이미지는 데이터 및 로그 디스크가으로 미리 구성 되어 있습니다. VM 데이터 디스크를 포함 하지 않은 hello VM 설치 프로세스 중 새 가상 하드 디스크를 추가 하는 경우 다음과 같이 hello 기본 폴더를 변경 합니다.
   
   * 왼쪽 패널 및 클릭 hello에 hello SQL 서버 이름 마우스 오른쪽 단추로 클릭 **속성**합니다.
     
       ![SQL Server 속성][14]
   * 선택 **데이터베이스 설정** hello에서 **페이지 선택** toohello 왼쪽을 나열 합니다.
   * 확인 및/또는 hello 변경 **데이터베이스 기본 위치** toohello **데이터 디스크** 위치를 선택 합니다. 기본 위치 설정을 hello 사용 하 여 만든 경우 새 데이터베이스가 상주 하는 위치입니다.
     
       ![SQL 데이터베이스 기본값][15]  
5. toocreate hello 분할 된 테이블, hello 샘플 스크립트를 열거나 새 데이터베이스 및 파일 그룹 toohold 집합이 **만들\_db\_default.sql**합니다. hello 스크립트 라는 새 데이터베이스를 만드는 **TaxiNYC** 및 hello 기본 데이터 위치에 12 파일 그룹입니다. 각 파일 그룹에는 한 달 분량의 trip\_data 및 trip\_fare 데이터가 유지됩니다. 필요한 경우 hello 데이터베이스 이름을 수정 합니다. 클릭 **! 실행** toorun hello 스크립트입니다.
6. 다음으로 hello 여정에 대해 하나씩 두 파티션 테이블을 만들고\_데이터와 hello 여정에 대해 다른\_요금입니다. Hello 샘플 스크립트를 열거나 **만들\_분할\_table.sql**, 것은:
   
   * 월별 파티션 함수 toosplit hello 데이터를 만듭니다.
   * 파티션 구성표 toomap 각 달의 데이터 tooa 다른 파일 그룹을 만듭니다.
   * 두 개의 분할 된 테이블의 매핑된 toohello 파티션 구성표 만들기: **nyctaxi\_여행** hello 여행이 포함 될\_데이터 및 **nyctaxi\_요금** hello 여행 보유 \_있어 데이터입니다.
     
     클릭 **! 실행** toorun 스크립트 hello 및 hello 분할 된 테이블을 만듭니다.
7. Hello에 **예제 스크립트** 폴더를 두 개의 샘플 PowerShell 스크립트 데이터 tooSQL 서버 테이블의 병렬 대량 가져오기를 toodemonstrate 제공 되는 합니다.
   
   * **bcp\_병렬\_generic.ps1** 은 일반 스크립트 tooparallel 대량 가져오기 데이터를 테이블에 있습니다. Hello 스크립트에 hello 주석 줄에 표시 된 대로이 스크립트 tooset hello 입력 및 대상 변수를 수정 합니다.
   * **bcp\_병렬\_nyctaxi.ps1** 미리 구성 된 버전의 hello 일반 스크립트 및 사용 되는 tootooload hello NYC 택시와 데이터에 대 한 두 일 수 있습니다.  
8. 마우스 오른쪽 단추로 클릭 hello **bcp\_병렬\_nyctaxi.ps1** 스크립트 이름 및 클릭 **편집** tooopen PowerShell에서 합니다. 검토 hello 변수 기본 설정 및 따라 tooyour 선택한 데이터베이스 이름, 입력된 데이터 폴더, 대상 로그 폴더 및 경로 toohello 예제 서식 파일 수정 **nyctaxi_trip.xml** 및 **nyctaxi\_ fare.xml** (hello에 제공 된 **예제 스크립트** 폴더).
   
    ![대용량 데이터 가져오기][16]
   
    Hello 인증 모드를 선택할 수 있습니다, 그리고 기본값은 Windows 인증입니다. 도구 모음 toorun hello에에서 hello 녹색 화살표를 클릭 합니다. hello 스크립트는 각 분할 된 테이블에 대 한 병렬, 12에서 24 대량 가져오기 작업을 시작 합니다. 위의 세트로 hello SQL Server 기본 데이터 폴더를 열어 hello 데이터 가져오기 진행률을 모니터링할 수 있습니다.
9. hello PowerShell 스크립트 보고서에는 시작 및 종료 시간 hello 합니다. 모든 대량 가져오기 완료, 종료 시간 hello 보고 됩니다. Hello 대상 로그 폴더에 보고 된 오류 없이 hello 대상 로그 폴더 tooverify hello 대량 가져오기 성공 했음을, 즉, 확인 합니다.
10. 이제 데이터베이스에서 탐색, 기능 엔지니어링 및 필요에 따라 다른 작업을 수행할 준비가 완료되었습니다. Hello 테이블이 toohello에 따라 분할 되는 이후 **픽업\_datetime** 필드를 포함 하는 쿼리 **픽업\_datetime** hello에 대 한 조건  **여기서** 절 hello 파티션 구성표에서 정보를 제공 합니다.
11. **SQL Server Management Studio**, 제공 된 hello 샘플 스크립트를 탐색 **샘플\_queries.sql**합니다. hello 샘플 쿼리를 강조 표시 hello 줄을 쿼리 한 다음 클릭 toorun **! 실행** hello 도구 모음에서입니다.
12. hello NYC 택시와 데이터는 두 개의 별도 테이블에 로드 됩니다. tooimprove 조인 작업 좋습니다 tooindex hello 테이블입니다. 샘플 스크립트 hello **만들\_분할\_index.sql** hello 복합 조인 키에서 분할 된 인덱스를 만듭니다. **메달 해킹\_라이선스 및 픽업\_datetime**합니다.

## <a name="dbexplore"></a>SQL Server에서 데이터 탐색 및 기능 엔지니어링
이 섹션에서는 hello에서 직접 SQL 쿼리를 실행 하 여 데이터 탐색 및 기능 생성을 수행 합니다 **SQL Server Management Studio** 앞에서 만든 hello SQL Server 데이터베이스를 사용 합니다. 라는 샘플 스크립트 **샘플\_queries.sql** hello에 제공 된 **예제 스크립트** 폴더입니다. Hello 기본값과에서 다른 경우 hello 스크립트 toochange hello 데이터베이스 이름, 수정: **TaxiNYC**합니다.

이 연습에서는 다음을 수행합니다.

* 너무 연결**SQL Server Management Studio** Windows 인증을 사용 하거나 SQL 인증 및 hello SQL 로그인 이름 및 암호를 사용 합니다.
* 다양한 기간에 걸쳐 몇몇 필드의 데이터 분포를 탐색합니다.
* Hello 경도 및 위도 필드의 데이터 품질을 조사 합니다.
* 이진 및 다중 클래스 분류 레이블을 hello에 따라 생성 **팁\_양**합니다.
* 기능을 생성하고 여정 거리를 계산/비교합니다.
* Hello 두 테이블을 조인 하 고 사용 하는 toobuild 모델 될 무작위 샘플링을 추출 합니다.

준비 tooproceed tooAzure 기계 학습을 있습니다 수 있습니다.  

1. Hello 최종 SQL 쿼리 tooextract 및 샘플 hello 데이터 및 복사-붙여넣기 hello에 직접 쿼리를 저장 한 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈 또는
2. 샘플링 hello 유지 및 엔지니어링된 데이터 toouse 새 데이터베이스에 작성 하는 모델에 대 한 계획 테이블 고 hello 새 테이블을 사용 하 여 hello에 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈입니다.

이 섹션의 hello 마지막 쿼리 tooextract 및 예제 hello 데이터 저장 됩니다. 두 번째 방법은 hello hello에 설명 된 [데이터 탐색 및 IPython 전자 필기장의 기능 엔지니어링](#ipnb) 섹션.

Hello hello의 행과 열 수의 빠른 확인 하기 위해 테이블 이전 병렬 대량 가져오기를 사용 하 여 입력

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>탐색: medallion별 여정 분포
이 예에서는 지정 된 기간 내에서 100 개 이상의 트립을 있는 hello 메달 (택시 번호)를 식별합니다. hello 쿼리는 것이 유리한 hello 분할 된 테이블 액세스에서의 파티션 구성표 hello 전제로 이후 **픽업\_datetime**합니다. Hello 전체 데이터 집합 쿼리 hello 분할 된 테이블의 사용 및/또는 색인 검색 또한 확인 됩니다.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>탐색: medallion 및 hack_license별 여정 분포
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>데이터 품질 평가: 경도 및/또는 위도가 잘못된 레코드 확인
이 예제에서는 조사 경우 잘못 된 값을 포함 하거나 hello 위도 및 경도 필드 (라디안 각도-90에서 90 사이의 이어야 함), 수도 있고 (0, 0) 좌표입니다.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>탐색: 왕복 여정과 비왕복 여정 분포
이 예제에서는 비교 크리스마스 된 기간에 (또는 hello 전체 데이터 집합의 hello 연도 포함 하는 경우) 지정된 된 시간에 크리스마스 하지와의 hello 수를 찾습니다. 이 배포는 나중에 이진 분류 모델링에 사용 하는 hello 이진 레이블 배포 toobe를 반영 합니다.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>탐색: 팁 클래스/범위 분포
이 예에서는 기간에 (또는 hello 전체 데이터 집합의 hello 연도 포함 하는 경우) 주어진된 시간에 팁 범위의 hello 분포를 계산 합니다. 다중 클래스 분류 모델링에 나중에 사용 하는 hello 레이블 클래스의 hello 분포입니다.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>탐색: 여정 거리 계산 및 비교
이 예제에서는 hello 픽업 및 자동 전송 경도 변환한 위도 tooSQL geography 가리키는 SQL geography 포인트 차이 사용 하 여 hello 여행 거리를 계산 하 고 비교에 대 한 hello 결과의 무작위 샘플링을 반환 합니다. hello 예제 toovalid만 앞에서 설명 하는 hello 데이터 품질 평가 쿼리를 사용 하 여 조정 하는 hello 결과 제한 합니다.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>SQL 쿼리의 기능 엔지니어링
hello 레이블 생성 및 geography 변환 탐색 쿼리 부분을 계산 하는 hello를 제거 하 여 사용 되는 toogenerate 레이블/기능 될 수도 있습니다. 추가 기능 엔지니어링 SQL 예 hello에 제공 됩니다 [데이터 탐색 및 IPython 전자 필기장의 기능 엔지니어링](#ipnb) 섹션. 것 hello 전체 데이터 집합 또는 SQL Server 데이터베이스 인스턴스 hello에서 직접 실행 하는 SQL 쿼리를 사용 하 여 큰 하위 집합에 더 효율적인 toorun hello 기능 생성 쿼리 합니다. hello 쿼리 실행할 수 **SQL Server Management Studio**, 로컬 또는 원격으로 IPython 노트북 또는 임의의 개발 도구/환경에 액세스할 수 있는 hello 데이터베이스입니다.

#### <a name="preparing-data-for-model-building"></a>모델 빌드를 위한 데이터 준비
hello 다음 쿼리는 조인 hello **nyctaxi\_여행** 및 **nyctaxi\_요금** 테이블, 이진 분류 레이블이 생성 **크리스마스**, 즉 다중 클래스 분류 레이블을 **팁\_클래스**, hello 전체 조인 된 데이터 집합에서 1% 무작위 샘플링을 추출 합니다. 이 쿼리를 복사 후 hello에 직접 붙여넣을 수 [Azure 기계 학습 스튜디오](https://studio.azureml.net) [데이터 가져오기] [ import-data] hello SQL Server 데이터베이스에서 직접 데이터 수집에 대 한 모듈 Azure의 인스턴스입니다. 잘못 된 레코드를 제외 하는 hello 쿼리 (0, 0) 좌표입니다.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>IPython Notebook에서 데이터 탐색 및 기능 엔지니어링
이 섹션에서는 데이터 탐색 및 앞에서 만든 hello SQL Server 데이터베이스에 대 한 Python와 SQL 쿼리를 사용 하 여 기능 생성을 수행 합니다. 명명 된 샘플 IPython 노트북 **machine-Learning-data-science-process-sql-story.ipynb** hello에 제공 된 **샘플 IPython 노트북** 폴더입니다. [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks)에서 이 Notebook을 사용할 수도 있습니다.

큰 데이터로 작업 하는 경우 시퀀스에 권장 하는 hello는 hello 다음:

* 메모리 내 데이터 프레임으로 hello 데이터의 작은 샘플에서 읽어옵니다.
* 일부 시각화 및 탐색 하는 hello 샘플링 된 데이터를 사용 하 여 수행 합니다.
* 데이터를 샘플링 하는 hello를 사용 하 여 기능 엔지니어링 놓습니다.
* 더 큰 데이터 탐색에 대 한 데이터 조작 및 기능 엔지니어링 hello Azure VM에서에서 Python tooissue SQL 쿼리 hello SQL Server 데이터베이스에 대해 직접 사용 합니다.
* Azure 기계 학습 모델 작성에 대 한 샘플 크기 toouse hello를 결정 합니다.

기계 학습 tooproceed tooAzure 준비 되 면, 하거나 수 있습니다.  

1. Hello 최종 SQL 쿼리 tooextract 및 샘플 hello 데이터 및 복사-붙여넣기 hello에 직접 쿼리를 저장 한 [데이터 가져오기] [ import-data] Azure 기계 학습의 모듈입니다. 이 메서드는 hello에 설명 된 [Azure 기계 학습에서 모델 작성](#mlmodel) 섹션.    
2. 샘플링 하는 hello와 새 데이터베이스 테이블에 작성 하는 모델에 대 한 toouse 계획 엔지니어링 된 데이터를 유지 다음 hello 새 테이블을 사용 하 여 hello에 [데이터 가져오기] [ import-data] 모듈입니다.

hello 다음은 몇 가지 데이터 탐색, 데이터 시각화 및 예제 엔지니어링 기능입니다. 더 많은 예제를 hello에서 hello 샘플 SQL IPython 노트북을 참조 하십시오. **샘플 IPython 노트북** 폴더입니다.

#### <a name="initialize-database-credentials"></a>데이터베이스 자격 증명 초기화
데이터베이스 연결 설정에서 다음 변수는 hello 초기화 합니다.

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>데이터베이스 연결 만들기
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>nyctaxi_trip 테이블의 행 및 열 수 보고
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* 총 행 수 = 173179759  
* 총 열 수 = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>읽기에 hello SQL Server 데이터베이스에서에서 작은 데이터 샘플
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

시간 tooread hello 예제 테이블은 6.492000 초  
검색된 행 및 열 수 = (84952, 21)

#### <a name="descriptive-statistics"></a>기술 통계
이제는 준비 tooexplore hello 샘플링 된 데이터입니다. Hello에 대 한 기술 통계를 살펴보면 가장 먼저 **여행\_거리** (또는 다른) 필드:

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>시각화: 상자 그림 예제
Hello 여행 거리 toovisualize hello 변 위치에 대 한 hello 상자 그림을 보면 다음

    df1.boxplot(column='trip_distance',return_type='dict')

![그릴 #1][1]

#### <a name="visualization-distribution-plot-example"></a>시각화: 분포 그림 예제
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![그릴 #2][2]

#### <a name="visualization-bar-and-line-plots"></a>시각화: 가로 막대형 및 꺾은선형 차트
이 예제에서는 hello 여행 거리 다섯 개의 bin으로 범주화 하 고 결과 범주화 하는 hello를 시각화 합니다.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Bin 분포 막대에서 위에 hello 그릴 하거나 아래와 같이 플롯을 줄 수 있습니다.

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![그릴 #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![그릴 #4][4]

#### <a name="visualization-scatterplot-example"></a>시각화: 산점도 예제
산 점도 간에 매개 변수를 표시 **여행\_시간\_에\_초** 및 **여행\_거리** toosee 상관 관계 없는 경우

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![그릴 #6][6]

Hello 관계 확인할 수 있습니다 마찬가지로 **속도\_코드** 및 **여행\_거리**합니다.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![그릴 #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a>하위 샘플링 hello SQL의 데이터
모델 빌드에 대 한 데이터를 준비할 때 [Azure 기계 학습 스튜디오](https://studio.azureml.net), 하거나 hello에 결정할 수 있습니다 **hello 데이터 가져오기 모듈에서 직접 SQL 쿼리 toouse** 하거나 hello 엔지니어링 및 샘플링 유지 hello에 사용할 수 있는 새 테이블의 데이터 [데이터 가져오기] [ import-data] 간단한을 사용 하 여 모듈 **선택 * FROM < 프로그램\_새\_테이블\_이름 >**합니다.

만듭니다이 섹션에서는 새 테이블 toohold hello 샘플링 하 고 데이터에 맞게 엔지니어링 되었습니다. Hello에 모델 작성에 대 한 직접 SQL 쿼리의 예제를 보려면 [데이터 탐색 및 SQL Server의 기능 엔지니어링](#dbexplore) 섹션.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>예제 테이블 및 채우기 hello 조인할 테이블의 1%로 만듭니다. 있는 경우 먼저 해당 테이블 삭제)
이 섹션에서는 hello 테이블 조인 **nyctaxi\_여행** 및 **nyctaxi\_요금**1% 무작위 샘플링을 추출 하 고 새 테이블 이름을 hello 샘플링 된 데이터를 유지,  **nyctaxi\_하나의\_%**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>IPython Notebook에서 SQL 쿼리를 사용하여 데이터 탐색
이 섹션에서는 위에서 만든 hello 새 테이블에서 유지 되는 hello 1% 샘플링 된 데이터를 사용 하 여 데이터 분포 탐색 합니다. 비슷한 탐색을 사용 하 여 필요에 따라 hello 원래 테이블을 사용 하 여 수행할 수 있도록 참고 **TABLESAMPLE** toolimit hello 탐색 샘플 또는 hello를 제한 하 여 결과 hello를 사용 하 여 시간 간격을 지정 하는 tooa **픽업 \_datetime** hello에 설명 된 대로 분할 [데이터 탐색 및 SQL Server의 기능 엔지니어링](#dbexplore) 섹션.

#### <a name="exploration-daily-distribution-of-trips"></a>탐색: 일일 여정 분포
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>탐색: medallion당 여정 분포
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>IPython Notebook에서 SQL 쿼리를 사용하여 기능 생성
이 섹션에 새 레이블을 생성 합니다 및 hello 이전 섹션에서 만든 SQL 쿼리를 사용 하 여 직접 기능을 hello 1% 예제 테이블에 대 한 작동 합니다.

#### <a name="label-generation-generate-class-labels"></a>레이블 생성: 클래스 레이블을 생성합니다.
다음 예제는 hello에서 두 가지 모델링에 대 한 레이블 toouse 생성:

1. 이진 클래스 레이블 **tipped** (팁이 제공되는지 예측)
2. 다중 클래스 레이블을 **팁\_클래스** (예측 hello 팁 bin 또는 범위)
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>기능 엔지니어링: 범주 열에 대한 개수 기능
이 예제에서는 해당 hello 데이터의 hello 개수와 각 범주를 대체 하 여 숫자 필드에 범주별 필드를 변환 합니다.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>기능 엔지니어링: 숫자 열에 대한 Bin 기능
이 예제에서는 연속 숫자 필드를 사전 설정된 범주 범위로 변환합니다. 즉, 숫자 필드를 범주 필드로 변환합니다.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>기능 엔지니어링: 10진수 위도/경도에서 위치 기능 추출
이 예제에서는 hello 위도 및 경도 필드의 10 진수 표현으로 분할 다양 한 세분성의 여러 지역 필드와 같은 국가, 도시, 동, 블록 등 됩니다. 아닌 hello 새 지역 필드는 tooactual 위치 매핑됩니다. 지오코드 위치 매핑에 대한 자세한 내용은 [Bing Maps REST 서비스](https://msdn.microsoft.com/library/ff701710.aspx)를 참조하세요.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Hello hello 들어가지 않고 기능화 테이블의 최종 형태를 확인 합니다.
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

준비 tooproceed toomodel 건물과 모델 배포에는 이제 [Azure 기계 학습](https://studio.azureml.net)합니다. hello 데이터는 즉 앞에서 확인 하는 hello 예측 문제에 대 한 준비:

1. 이진 분류: toopredict 트립이 팁 지불 여부.
2. 다중 클래스 분류: toohello 이전에 정의 된 클래스에 따라 지불을 끝의 toopredict hello 범위입니다.
3. 회귀 작업: toopredict hello 양을 팁은 여행에 대 한 지불 합니다.  

## <a name="mlmodel"></a>Azure 기계 학습에서 모델 빌드
toobegin hello 모델링 연습 tooyour Azure 기계 학습 작업 영역에 로그인 합니다. 기계 학습 작업 영역을 아직 만들지 않은 경우 [Azure 기계 학습 작업 영역 만들기](machine-learning-create-workspace.md)를 참조하세요.

1. Azure 기계 학습 시작 tooget 참조 [Azure 기계 학습 스튜디오는 무엇입니까?](machine-learning-what-is-ml-studio.md)
2. 로그 너무[Azure 기계 학습 스튜디오](https://studio.azureml.net)합니다.
3. hello Studio 홈 페이지는 다양 한 정보, 비디오, 자습서, 링크 toohello 모듈 참조 및 기타 리소스를 제공합니다. Azure 기계 학습에 대 한 자세한 내용은 hello를 참조 하십시오. [Azure 기계 학습 설명서 센터](https://azure.microsoft.com/documentation/services/machine-learning/)합니다.

일반적인 학습 실험 hello 다음 이루어져 있습니다.

1. **+새** 실험 만들기
2. Hello 데이터 tooAzure를 기계 학습을 가져옵니다.
3. 전처리 하 고, 변환 및 필요에 따라 hello 데이터를 조작 합니다.
4. 필요에 따라 기능을 생성합니다.
5. Hello 데이터를 학습 /, 유효성 검사, 테스트 데이터 집합 분할 (별도 데이터 집합 수도 있고 각각에 대해).
6. 하나 이상의 기계 학습 문제 toosolve 학습 hello에 따라 알고리즘을 선택 합니다. 이진 분류, 다중 클래스 분류, 회귀)을 선택합니다.
7. Hello 학습 데이터 집합을 사용 하 여 하나 이상의 모델을 학습 합니다.
8. Hello 학습 된 모델을 사용 하 여 hello 유효성 검사 데이터 집합을 점수를 매깁니다.
9. Hello 모델로 toocompute hello 관련 메트릭 hello 학습 문제에 대 한 평가 합니다.
10. Hello 모델 및 선택 hello 최상의 모델 toodeploy 미세 조정 합니다.

이 연습에서는 이미 탐색 하 고 SQL Server에서 hello 데이터 엔지니어링 했으며 hello 샘플 크기 tooingest Azure 기계 학습에서 결정 합니다. 하나 이상의 hello 예측 모델 toobuild 결정 했습니다.

1. Hello 데이터 tooAzure 기계 학습 가져오기 hello를 사용 하 여 [데이터 가져오기] [ import-data] hello에서 사용할 수 있는 모듈 **데이터 입력 및 출력** 섹션. 자세한 내용은 참조 hello [데이터 가져오기] [ import-data] 모듈 참조 페이지입니다.
   
    ![Azure 기계 학습 데이터 가져오기][17]
2. 선택 **Azure SQL 데이터베이스** hello로 **데이터 소스** hello에 **속성** 패널입니다.
3. Hello에 hello 데이터베이스 DNS 이름을 입력 **데이터베이스 서버 이름** 필드입니다. 형식: `tcp:<your_virtual_machine_DNS_name>,1433`
4. Hello 입력 **데이터베이스 이름** hello 해당 필드에 있습니다.
5. Hello 입력 **SQL 사용자 이름** hello에서 * * 서버 사용자 aqccount 이름 및 hello에 hello 암호 **서버 사용자 계정 암호**합니다.
6. **모든 서버 인증서 허용** 옵션을 선택합니다.
7. Hello에 **데이터베이스 쿼리** 텍스트 영역을 편집, hello 필요한 데이터베이스 필드 (예: hello 레이블 모든 계산된 필드 포함), 아래에 추출 hello 데이터 원하는 toohello 샘플 크기를 샘플링 하는 hello 쿼리를 붙여 넣습니다.

아래 hello 그림에 hello SQL Server 데이터베이스에서 직접 데이터를 읽는 이진 분류 실험의 예가입니다. 다중 클래스 분류 및 회귀 문제에 대한 유사한 실험을 생성할 수 있습니다.

![Azure 기계 학습][10]

> [!IMPORTANT]
> 데이터 추출을 모델링 하 고 이전 섹션에서 제공 하는 쿼리 예제 샘플링 hello에 **hello 3 모델링 연습에 대 한 모든 레이블을 hello 쿼리에 포함 된**합니다. 각 연습을 모델링 하는 hello (필수) 중요 한 단계는 너무**제외** 다른 두 가지 문제 및 기타 hello에 대 한 불필요 한 레이블을 hello **누수 대상**합니다. 에 대 한 예: 이진 분류를 사용할 때 사용 하 여 hello 레이블 **크리스마스** hello 필드를 제외 하 고 **팁\_클래스**, **팁\_양**, 및 **총\_양**합니다. 후자의 hello 대상 누수 hello 팁 사실도 지불 됩니다.
> 
> hello tooexclude 불필요 한 열 및/또는 대상 누수를 사용할 수 있습니다 [데이터 집합의 열 선택] [ select-columns] 모듈 또는 hello [메타 데이터 편집] [ edit-metadata]. 자세한 내용은 [데이터 집합의 열 선택][select-columns] 및 [메타데이터 편집][edit-metadata] 참조 페이지를 참조하세요.
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

실험 점수 매기기 hello 만들어지면 검토 하 고 필요에 따라 조정 합니다. 이러한 표시 되지 것입니다 hello 서비스를 호출 하는 경우 일반적인 조정은 tooreplace hello 입력된 데이터 집합 및/또는 레이블 필드를 제외를 사용 하 여 쿼리 합니다. 것이 좋습니다 tooreduce hello 크기인 hello 입력 데이터 집합 및/또는 쿼리 tooa 소수의 레코드 데 충분 한 tooindicate hello 입력된 스키마도입니다. Hello 출력 포트에 대 한 일반적인 tooexclude 모든 입력된 필드 이며 hello 포함 **점수가 매겨진 레이블** 및 **점수가 매겨진 확률** hello hello를 사용 하 여 출력에 [데이터 집합의 열 선택 ] [ select-columns] 모듈입니다.

샘플 실험을 점수 매기기 아래 hello 그림에 있는 경우 Toodeploy, 준비 되 면 hello 클릭 **웹 서비스 게시** hello 낮은 작업 모음에서 단추입니다.

![Azure 기계 학습 게시][11]

toorecap,이 연습에서는 자습서에서 큰 공용 데이터 집합 데이터 취득 toomodel 학습 및 Azure 기계 학습 웹 서비스의 배포에서 모든 hello 방법에 대해 작업 하는 Azure 데이터 과학 환경을 만들었습니다.

### <a name="license-information"></a>라이선스 정보
이 샘플 연습 및 그에 따른 스크립트 및 IPython notebook(s)은 hello MIT 라이선스에 따라 Microsoft에서 공유 됩니다. 자세한 내용은 GitHub에서 hello 샘플 코드의 hello 디렉터리에 hello LICENSE.txt 파일 확인 하십시오.

### <a name="references"></a>참조
• [Andrés Monroy NYC Taxi Trips 다운로드 페이지](http://www.andresmh.com/nyctaxitrips/)  
• [Chris Whong의 FOILing NYC Taxi Trip 데이터](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC Taxi 및 Limousine 수수료 연구 및 통계](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
