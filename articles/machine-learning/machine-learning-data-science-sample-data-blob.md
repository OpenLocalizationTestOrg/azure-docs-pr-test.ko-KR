---
title: "Azure에서 aaaSample 데이터 blob 저장소 | Microsoft Docs"
description: "Azure Blob 저장소에서 데이터 샘플링"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Azure Blob 저장소에서 데이터 샘플링
이 문서에서는 프로그래밍 방식으로 다운로드한 다음 Python으로 작성된 절차에 따라 샘플링하여 Azure Blob 저장소에 저장된 데이터를 샘플링하는 방법에 대해 알아봅니다.

hello 다음 **메뉴** tootopics 설명 하는 연결 방법을 다양 한 저장소 환경에서 toosample 데이터입니다. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**데이터를 샘플링하는 이유**
Tooanalyze 계획 hello 데이터 집합이 크면 경우 일반적으로 좋습니다 toodown 샘플 hello 데이터 tooreduce 것 tooa 있지만 대표 작고 더 관리 가능한 수치로 크기입니다. 그러면 데이터 이해, 탐색 및 기능 엔지니어링이 용이해집니다. Hello Cortana 분석 프로세스에서에서 해당 역할에는 데이터 처리 함수 hello 및 기계 학습 모델의 tooenable 빠르게 프로토타입을 만들입니다.

이 샘플링 작업은 hello 단계 [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)합니다.

## <a name="download-and-down-sample-data"></a>데이터 다운로드 및 저해상도로 처리
1. 다음 샘플 Python 코드가 hello에서 hello blob 서비스를 사용 하 여 Azure blob 저장소에서 hello 데이터를 다운로드 합니다. 
   
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

2. 팬더 데이터-프레임으로 위의 다운로드 hello 파일에서 데이터를 읽습니다.
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. 하위 키를 누른 채 샘플 hello를 사용 하 여 hello 데이터 `numpy`의 `random.choice` 다음과 같습니다.
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

이제 따르는 것이 고 기능 생성에 대 한 hello 1 퍼센트 샘플을 사용 하 여 데이터 프레임 위의 hello로 작업할 수 있습니다.

## <a name="heading"></a>데이터 업로드 및 Azure 기계 학습으로 읽어오기
다음 샘플 코드 toodown 샘플 hello 데이터 hello를 사용 하 여 및 Azure 기계 학습에서 직접 사용할 수 있습니다.

1. Hello 데이터 프레임 tooa 로컬 파일 쓰기
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. Azure의 hello 로컬 파일 tooan 업로드 hello 다음 샘플 코드를 사용 하 여 blob:
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. Hello Azure 기계 학습을 사용 하 여 Azure blob에서에서 hello 데이터 읽기 [데이터 가져오기](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) hello 이미지 아래에 나와 있는 것 처럼:

![판독기 blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

