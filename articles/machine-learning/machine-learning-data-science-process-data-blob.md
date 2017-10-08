---
title: "Azure aaaProcess 고급 분석을 사용 하 여 데이터를 blob | Microsoft Docs"
description: "Azure Blob 저장소에서 데이터 처리"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>고급 분석을 사용하여 Azure blob 데이터 처리
이 문서에서는 Azure Blob 저장소에 저장된 데이터를 탐색하고 기능을 생성하는 방법을 다룹니다. 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>팬더 데이터 프레임으로 hello 데이터 로드
순서 tooexplore에서 데이터 집합을 조작 하 고, hello blob 원본 tooa 로컬 파일에서 다음 팬더 데이터 프레임에서 로드할 수 있는 다운로드 해야 합니다. 이 절차에 대 한 hello 단계 toofollow 다음과 같습니다.

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

## <a name="blob-dataexploration"></a>데이터 탐색
다음 방법 중 몇 가지 예를 팬더를 사용 하 여 tooexplore 데이터는:

1. Hello 개수의 행과 열을 검사 합니다. 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. Hello를 먼저 검사 만들거나 아래와 같이 hello 데이터 집합의 행 몇 마지막:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. 각 열에서 가져온 다음 샘플 코드는 hello를 사용 하 여 hello 데이터 형식을 확인합니다
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. 확인 hello hello 데이터 집합의 hello 열에 대 한 기본 통계 방법
   
        dataframe_blobdata.describe()
5. 다음과 같이 hello 각 열 값에 대 한 항목 수 확인
   
        dataframe_blobdata['<column_name>'].value_counts()
6. 다음 샘플 코드는 hello를 사용 하 여 각 열에 있는 항목의 hello 실제 수와 누락 된 값 계산
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Hello 데이터를 특정 열에 대 한 누락 된 값이 있을 경우에 다음과 같이 삭제할 수 있습니다.
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   또 다른 방법은 tooreplace 누락 된 값은 hello 모드 함수:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. 다양 한 수의 bin tooplot hello 배포 변수를 사용 하 여 히스토그램 점도 만들기    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. scatterplot 또는 hello 상관 관계 기본 제공 함수를 사용 하 여 변수 간의 상관 관계 확인
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>기능 생성
다음과 같이 Python을 사용하여 기능을 생성할 수 있습니다.

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
3. Hello 데이터를 사용 하 여 hello blob에서 읽을 수 이제 hello Azure 기계 학습 [데이터 가져오기] [ import-data] hello 화면 아래에 나와 있는 것 처럼 모듈:

![판독기 blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

