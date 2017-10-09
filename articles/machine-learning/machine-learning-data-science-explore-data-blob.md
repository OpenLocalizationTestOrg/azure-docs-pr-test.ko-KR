---
title: "Azure에서 aaaExplore 데이터 blob 저장소와 팬더 | Microsoft Docs"
description: "어떻게 tooexplore 저장 된 데이터를 Azure에서 blob 팬더를 사용 하 여 컨테이너입니다."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Pandas를 사용하여 Azure Blob 저장소의 데이터 탐색
이 문서에서는 Azure에 저장 된 tooexplore 데이터 blob 컨테이너를 사용 하 여 하는 방법을 설명 [팬더](http://pandas.pydata.org/) Python 패키지 합니다.

hello 다음 **메뉴** tootopics toouse 도구 tooexplore 데이터 저장소, 다양 한 환경에서 하는 방법을 설명 하는 링크입니다. 이 작업은 hello 단계 [데이터 과학 프로세스]()합니다.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>필수 조건
이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.

* Azure 저장소 계정을 만들었습니다. 지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.
* Azure Blob 저장소 계정에 데이터를 저장합니다. 지침이 필요한 경우 참조 [Azure 저장소에서 데이터 tooand 이동](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>팬더 데이터 프레임이 hello 데이터 로드
tooexplore 데이터 집합을 조작 하 고, hello blob 원본 tooa 로컬 파일에서 다음 팬더 데이터 프레임에서 로드할 수 있는 먼저 다운로드 해야 합니다. 이 절차에 대 한 hello 단계 toofollow 다음과 같습니다.

1. Azure의 hello 데이터 다운로드 아래의 blob 서비스를 사용 하 여 Python 코드 예제는 hello로 blob입니다. Hello 변수에 특정 값으로 코드 다음 hello 바꿉니다. 
   
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

## <a name="blob-dataexploration"></a>Pandas를 사용 하 여 데이터 탐색의 예
다음 방법 중 몇 가지 예를 팬더를 사용 하 여 tooexplore 데이터는:

1. Hello 검사 **의 행과 열 번호** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **검사** 첫 번째 또는 마지막 몇 개의 hello **행** hello 데이터 집합 뒤에:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Hello 확인 **데이터 형식을** 각 열에서 가져온 다음 샘플 코드는 hello를 사용 하 여
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Hello 확인 **기본 통계** hello 열에서 데이터 집합을 다음과 같이 hello에 대 한
   
        dataframe_blobdata.describe()
5. 다음과 같이 hello 각 열 값에 대 한 항목 수 확인
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **누락 값 개수** 와 hello hello 다음 샘플 코드를 사용 하 여 각 열에 있는 항목의 실제 수
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. 있는 경우 **누락 값** hello 데이터의 특정 열에 대 한 수 스키마를 삭제 하면 다음과 같습니다.
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   또 다른 방법은 tooreplace 누락 된 값은 hello 모드 함수:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. 만들기는 **히스토그램** 가변 개수의 변수의 bin tooplot hello 배포를 사용 하 여 플롯    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. 살펴보고 **상관 관계** 는 scatterplot 또는 hello 상관 관계 기본 제공 함수를 사용 하 여 변수 간의
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

