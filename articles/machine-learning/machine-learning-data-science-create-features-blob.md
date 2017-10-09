---
title: "Azure에 대 한 aaaCreate 기능 팬더를 사용 하 여 저장소 데이터를 blob | Microsoft Docs"
description: "Toocreate는 hello 팬더 Python 패키지를 사용 하 여 Azure blob 컨테이너에 저장 된 데이터에 대 한 기능이 방법입니다."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Panda를 사용하여 Azure blob 저장소 데이터에 대한 기능 만들기
이 문서에서는 toocreate hello를 사용 하 여 Azure blob 컨테이너에 저장 된 데이터에 대 한 기능 하는 방법을 보여 줍니다. [팬더](http://pandas.pydata.org/) Python 패키지 합니다. 개요 어떻게 팬더 데이터 프레임으로 tooload hello 데이터를 표시 한 후 어떻게 toogenerate 범주 기능 표시기 값이 포함 된 Python 스크립트를 사용 하 고 기능을 범주화 합니다.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

이 **메뉴** tootopics toocreate 다양 한 환경에서 데이터에 대 한 기능 하는 방법을 설명 하는 링크입니다. 이 작업은 hello 단계 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.

## <a name="prerequisites"></a>필수 조건
이 문서에서는 Azure blob 저장소 계정을 만들고 여기에 데이터를 저장했다고 가정합니다. 계정을 지침 tooset 필요한 경우 참조 [Azure 저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>팬더 데이터 프레임으로 hello 데이터 로드
순서 toodo을 탐색 하 고 데이터 집합을 조작, hello blob 원본 tooa 로컬 파일에서 다음 팬더 데이터 프레임에서 로드할 수 있는 다운로드 해야 합니다. 이 절차에 대 한 hello 단계 toofollow 다음과 같습니다.

1. Azure의 hello 데이터 다운로드 샘플 Python 코드가 blob 서비스를 사용 하 여 다음 hello로 blob입니다. 아래 hello 코드의 hello 변수를 특정 값으로 바꿉니다.
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. Hello에서 팬더 데이터 프레임을으로 읽기 hello 데이터 파일을 다운로드 합니다.
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

이제는 준비 tooexplore hello 데이터와이 데이터 집합에서 기능을 생성 합니다.

## <a name="blob-featuregen"></a>기능 생성
hello 다음 두 사항을 표시기 값 및 범주화 toogenerate 범주 기능 Python 스크립트를 사용 하는 기능 방법을 보여 줍니다.

### <a name="blob-countfeature"></a>표시기 값 기반 기능 생성
범주 기능은 다음과 같은 방법으로 만들 수 있습니다.

1. Hello 범주 열의 hello 분포를 검사 합니다.
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. 각 hello 열 값에 대 한 표시기 값을 생성 합니다.
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. 원래 데이터 프레임 hello hello 표시기 열 조인
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Hello 원래 변수 자체를 제거 합니다.
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>범주화 기능 생성
범주화된 기능을 생성하려면 다음 단계를 진행합니다.

1. 숫자 열의 열 toobin의 시퀀스를 추가 합니다.
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. 범주화 tooa 시퀀스의 부울 변수 변환 합니다.
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. 조인 hello 더미 변수 toohello 원래 데이터 프레임을 백업 하는 마지막으로,
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <a name="sql-featuregen"></a>쓰기 데이터 다시 tooAzure blob 및 Azure 기계 학습에서 사용
Hello 데이터를 탐색 하 고 필요한 기능 hello를 만든 후 hello 데이터를 업로드할 수 있습니다 (샘플링 또는 들어가지 않고 기능화) tooan Azure blob 및 단계를 수행 하는 hello를 사용 하 여 Azure 기계 학습에서 사용: hello에 추가 기능을 만들 수 있음을 확인 합니다. Azure 기계 학습 스튜디오도 합니다.

1. Hello 데이터 프레임 toolocal 파일 쓰기
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. 다음과 같이 hello 데이터 tooAzure blob을 업로드 합니다.
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. Hello 데이터를 사용 하 여 hello blob에서 읽을 수 이제 hello Azure 기계 학습 [데이터 가져오기](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) hello 화면 아래에 나와 있는 것 처럼 모듈:

![판독기 blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

