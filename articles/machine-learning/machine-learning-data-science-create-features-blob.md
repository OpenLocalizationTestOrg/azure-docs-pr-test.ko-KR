---
title: "Panda를 사용하여 Azure Blob Storage 데이터에 대한 기능 만들기 | Microsoft Docs"
description: "Panda Python 패키지를 사용하여 Azure blob 컨테이너에 저장된 데이터에 대한 기능을 만드는 방법"
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
ms.openlocfilehash: 2ef2acfea2372ac7fd52d099a2b4203ee2242d81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="e1150-103">Panda를 사용하여 Azure blob 저장소 데이터에 대한 기능 만들기</span><span class="sxs-lookup"><span data-stu-id="e1150-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="e1150-104">이 문서는 [Panda](http://pandas.pydata.org/) Python 패키지를 사용하여 Azure Blob 컨테이너에 저장된 데이터에 대한 기능을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="e1150-105">Panda 데이터 프레임에 데이터를 로드하는 방법을 설명한 후, 표시기 값과 범주화 기능과 함께 Python 스크립트를 사용하여 범주 기능을 생성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="e1150-106">이 **메뉴** 는 다양한 환경에서 데이터에 대한 기능을 만드는 방법을 설명하는 토픽으로 연결되는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="e1150-107">이 작업은 [TDSP(팀 데이터 과학 프로세스)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1150-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e1150-108">Prerequisites</span></span>
<span data-ttu-id="e1150-109">이 문서에서는 Azure blob 저장소 계정을 만들고 여기에 데이터를 저장했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="e1150-110">계정을 설정하는 지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1150-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="e1150-111">Pandas 데이터 프레임에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="e1150-111">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="e1150-112">데이터 집합을 탐색 및 조작하려면 Blob 원본에서 로컬 파일로 다운로드한 다음 Pandas 데이터 프레임에 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="e1150-113">이 절차를 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-113">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="e1150-114">blob 서비스를 사용하여 다음 샘플 Python 코드로 Azure blob에서 데이터를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-114">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="e1150-115">아래의 코드 변수를 사용자가 원하는 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-115">Replace the variable in the code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="e1150-116">다운로드한 파일에서 데이터를 Pandas 데이터 프레임으로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-116">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="e1150-117">이제 데이터를 탐색하고 이 데이터 집합에 기능을 생성할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-117">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="e1150-118"><a name="blob-featuregen"></a>기능 생성</span><span class="sxs-lookup"><span data-stu-id="e1150-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="e1150-119">다음 두 섹션에는 Python 스크립트를 사용하여 표시기 값과 범주화 기능으로 범주 기능을 생성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="e1150-120"><a name="blob-countfeature"></a>표시기 값 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="e1150-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="e1150-121">범주 기능은 다음과 같은 방법으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="e1150-122">범주 열의 분포를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-122">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="e1150-123">각 열 값에 대한 표시기 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-123">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="e1150-124">표시기 열을 원래 데이터 프레임에 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-124">Join the indicator column with the original data frame</span></span>
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="e1150-125">원래 변수 자체를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-125">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="e1150-126"><a name="blob-binningfeature"></a>범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="e1150-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="e1150-127">범주화된 기능을 생성하려면 다음 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="e1150-128">열 시퀀스를 추가하여 숫자 열을 범주화합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-128">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="e1150-129">범주화를 부울 변수 시퀀스로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-129">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="e1150-130">마지막으로 더미 변수를 다시 원래 데이터 프레임에 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-130">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="e1150-131"><a name="sql-featuregen"></a>다시 Azure blob에 데이터를 쓰고 Azure 기계 학습에서 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="e1150-131"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="e1150-132">데이터를 탐색하고 필요한 기능을 만든 후에는 다음 단계에 따라 샘플링한 또는 기능화한 데이터를 Azure blob에 업로드하여 Azure 기계 학습에서 사용할 수 있습니다. Azure 기계 학습 스튜디오에서 추가 기능을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="e1150-133">로컬 파일에 데이터 프레임을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-133">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="e1150-134">다음과 같이 Azure blob에 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-134">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="e1150-135">이제 아래 그림과 같이 Azure 기계 학습 [데이터 가져오기](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) 모듈을 사용하여 blob에서 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1150-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span></span>

![판독기 blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

