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
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="a5879-103">Pandas를 사용하여 Azure Blob 저장소의 데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="a5879-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="a5879-104">이 문서에서는 Azure에 저장 된 tooexplore 데이터 blob 컨테이너를 사용 하 여 하는 방법을 설명 [팬더](http://pandas.pydata.org/) Python 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="a5879-105">hello 다음 **메뉴** tootopics toouse 도구 tooexplore 데이터 저장소, 다양 한 환경에서 하는 방법을 설명 하는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="a5879-106">이 작업은 hello 단계 [데이터 과학 프로세스]()합니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="a5879-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a5879-107">Prerequisites</span></span>
<span data-ttu-id="a5879-108">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-108">This article assumes that you have:</span></span>

* <span data-ttu-id="a5879-109">Azure 저장소 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-109">Created an Azure storage account.</span></span> <span data-ttu-id="a5879-110">지침이 필요한 경우 [Azure Storage 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5879-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="a5879-111">Azure Blob 저장소 계정에 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="a5879-112">지침이 필요한 경우 참조 [Azure 저장소에서 데이터 tooand 이동](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="a5879-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="a5879-113">팬더 데이터 프레임이 hello 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="a5879-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="a5879-114">tooexplore 데이터 집합을 조작 하 고, hello blob 원본 tooa 로컬 파일에서 다음 팬더 데이터 프레임에서 로드할 수 있는 먼저 다운로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="a5879-115">이 절차에 대 한 hello 단계 toofollow 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="a5879-116">Azure의 hello 데이터 다운로드 아래의 blob 서비스를 사용 하 여 Python 코드 예제는 hello로 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="a5879-117">Hello 변수에 특정 값으로 코드 다음 hello 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="a5879-118">Hello에서 팬더 데이터 프레임을으로 읽기 hello 데이터 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="a5879-119">이제는 준비 tooexplore hello 데이터와이 데이터 집합에서 기능을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="a5879-120"><a name="blob-dataexploration"></a>Pandas를 사용 하 여 데이터 탐색의 예</span><span class="sxs-lookup"><span data-stu-id="a5879-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="a5879-121">다음 방법 중 몇 가지 예를 팬더를 사용 하 여 tooexplore 데이터는:</span><span class="sxs-lookup"><span data-stu-id="a5879-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="a5879-122">Hello 검사 **의 행과 열 번호**</span><span class="sxs-lookup"><span data-stu-id="a5879-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="a5879-123">**검사** 첫 번째 또는 마지막 몇 개의 hello **행** hello 데이터 집합 뒤에:</span><span class="sxs-lookup"><span data-stu-id="a5879-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="a5879-124">Hello 확인 **데이터 형식을** 각 열에서 가져온 다음 샘플 코드는 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a5879-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="a5879-125">Hello 확인 **기본 통계** hello 열에서 데이터 집합을 다음과 같이 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="a5879-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="a5879-126">다음과 같이 hello 각 열 값에 대 한 항목 수 확인</span><span class="sxs-lookup"><span data-stu-id="a5879-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="a5879-127">**누락 값 개수** 와 hello hello 다음 샘플 코드를 사용 하 여 각 열에 있는 항목의 실제 수</span><span class="sxs-lookup"><span data-stu-id="a5879-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="a5879-128">있는 경우 **누락 값** hello 데이터의 특정 열에 대 한 수 스키마를 삭제 하면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5879-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="a5879-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="a5879-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="a5879-130">또 다른 방법은 tooreplace 누락 된 값은 hello 모드 함수:</span><span class="sxs-lookup"><span data-stu-id="a5879-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="a5879-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="a5879-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="a5879-132">만들기는 **히스토그램** 가변 개수의 변수의 bin tooplot hello 배포를 사용 하 여 플롯</span><span class="sxs-lookup"><span data-stu-id="a5879-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="a5879-133">살펴보고 **상관 관계** 는 scatterplot 또는 hello 상관 관계 기본 제공 함수를 사용 하 여 변수 간의</span><span class="sxs-lookup"><span data-stu-id="a5879-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

