---
title: "Azure Blob Storage에서 데이터 샘플링 | Microsoft Docs"
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
ms.openlocfilehash: aa9ab454706429682a393c3d5758cebe20790e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="07395-103"><a name="heading"></a>Azure Blob 저장소에서 데이터 샘플링</span><span class="sxs-lookup"><span data-stu-id="07395-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="07395-104">이 문서에서는 프로그래밍 방식으로 다운로드한 다음 Python으로 작성된 절차에 따라 샘플링하여 Azure Blob 저장소에 저장된 데이터를 샘플링하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="07395-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="07395-105">다음의 **메뉴** 는 다양한 저장소 환경에서 데이터를 샘플링하는 방법을 설명하는 토픽에 연결되는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="07395-105">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="07395-106">**데이터를 샘플링하는 이유**</span><span class="sxs-lookup"><span data-stu-id="07395-106">**Why sample your data?**</span></span>
<span data-ttu-id="07395-107">분석할 데이터 집합이 큰 경우 일반적으로 데이터를 다운 샘플링하여 작지만 전형적이고 관리하기 쉬운 크기로 줄이는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="07395-107">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="07395-108">그러면 데이터 이해, 탐색 및 기능 엔지니어링이 용이해집니다.</span><span class="sxs-lookup"><span data-stu-id="07395-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="07395-109">Cortana 분석 프로세스에서는 데이터 처리 기능 및 기계 학습 모델의 빠른 프로토타입 제작을 지원하는 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="07395-109">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="07395-110">이 샘플 작업은 [TDSP(팀 데이터 과학 프로세스)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="07395-110">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="07395-111">데이터 다운로드 및 저해상도로 처리</span><span class="sxs-lookup"><span data-stu-id="07395-111">Download and down-sample data</span></span>
1. <span data-ttu-id="07395-112">다음 샘플 Python 코드에서 Blob 서비스를 사용하여 Azure Blob 저장소에서 데이터를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="07395-112">Download the data from Azure blob storage using the blob service from the following sample Python code:</span></span> 
   
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
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))

2. <span data-ttu-id="07395-113">다운로드한 파일에서 Pandas 데이터 프레임으로 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="07395-113">Read data into a Pandas data-frame from the file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="07395-114">다음과 같이 `numpy`의 `random.choice`를 사용하여 데이터를 저해상도로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="07395-114">Down-sample the data using the `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="07395-115">이제 추가 탐색 및 기능 생성을 위해 1% 샘플을 사용하여 위의 데이터 프레임으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07395-115">Now you can work with the above data frame with the 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="07395-116"><a name="heading"></a>데이터 업로드 및 Azure 기계 학습으로 읽어오기</span><span class="sxs-lookup"><span data-stu-id="07395-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="07395-117">다음 샘플 코드를 사용하여 데이터를 다운 샘플링하고 Azure 기계 학습에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07395-117">You can use the following sample code to down-sample the data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="07395-118">데이터 프레임을 로컬 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="07395-118">Write the data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="07395-119">다음 샘플 코드를 사용하여 Azure Blob에 로컬 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="07395-119">Upload the local file to an Azure blob using the following sample code:</span></span>
   
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
            print ("Something went wrong with uploading to the blob:"+ BLOBNAME)

3. <span data-ttu-id="07395-120">아래 이미지에 표시된 대로 Azure 기계 학습 [데이터 가져오기](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 를 사용하여 Azure Blob에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="07395-120">Read the data from the Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in the image below:</span></span>

![판독기 blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

