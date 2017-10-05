---
title: "고급 분석을 사용하여 Azure Blob 데이터 처리 | Microsoft Docs"
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
ms.openlocfilehash: 36d950fd81029af82d9f2f652b2f01dba5fc8cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="9c12c-103"><a name="heading"></a>고급 분석을 사용하여 Azure blob 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="9c12c-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="9c12c-104">이 문서에서는 Azure Blob 저장소에 저장된 데이터를 탐색하고 기능을 생성하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="9c12c-105">Pandas 데이터 프레임에 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="9c12c-105">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="9c12c-106">데이터 집합을 탐색 및 조작하려면 Blob 원본에서 로컬 파일로 다운로드한 다음 Pandas 데이터 프레임에 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="9c12c-107">이 절차를 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-107">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="9c12c-108">blob 서비스를 사용하여 다음 샘플 Python 코드로 Azure blob에서 데이터를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-108">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="9c12c-109">아래의 코드 변수를 사용자가 원하는 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-109">Replace the variable in the code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="9c12c-110">다운로드한 파일에서 데이터를 Pandas 데이터 프레임으로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-110">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="9c12c-111">이제 데이터를 탐색하고 이 데이터 집합에 기능을 생성할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-111">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="9c12c-112"><a name="blob-dataexploration"></a>데이터 탐색</span><span class="sxs-lookup"><span data-stu-id="9c12c-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="9c12c-113">다음은 Pandas를 사용하여 데이터를 탐색하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-113">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="9c12c-114">행 및 열 수를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-114">Inspect the number of rows and columns</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="9c12c-115">아래와 같이 데이터 집합의 처음 또는 마지막 몇 행을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-115">Inspect the first or last few rows in the dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="9c12c-116">다음 샘플 코드를 사용하여 각 열을 가져온 데이터 유형을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-116">Check the data type each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="9c12c-117">다음과 같이 데이터 집합의 열에 대한 기본 통계를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-117">Check the basic stats for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="9c12c-118">다음과 같이 각 열 값에 대한 항목 수를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-118">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="9c12c-119">다음 샘플 코드를 사용하여 각 열의 실제 항목 수와 누락된 값을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-119">Count missing values versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="9c12c-120">데이터의 특정 열에 대한 값이 누락된 경우 다음과 같이 해당 데이터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-120">If you have missing values for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="9c12c-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="9c12c-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="9c12c-122">누락된 값을 대체하는 또 다른 방법으로 mode 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-122">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="9c12c-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="9c12c-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="9c12c-124">가변 bin을 사용하여 히스토그램 플롯을 만들고 변수 분포 그리기</span><span class="sxs-lookup"><span data-stu-id="9c12c-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="9c12c-125">산점도 또는 기본 제공 상관관계 함수를 사용하여 변수 간의 상관관계를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="9c12c-126"><a name="blob-featuregen"></a>기능 생성</span><span class="sxs-lookup"><span data-stu-id="9c12c-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="9c12c-127">다음과 같이 Python을 사용하여 기능을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="9c12c-128"><a name="blob-countfeature"></a>표시기 값 기반 기능 생성</span><span class="sxs-lookup"><span data-stu-id="9c12c-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="9c12c-129">범주 기능은 다음과 같은 방법으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="9c12c-130">범주 열의 분포를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-130">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="9c12c-131">각 열 값에 대한 표시기 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-131">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="9c12c-132">표시기 열을 원래 데이터 프레임에 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-132">Join the indicator column with the original data frame</span></span> 
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="9c12c-133">원래 변수 자체를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-133">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="9c12c-134"><a name="blob-binningfeature"></a>범주화 기능 생성</span><span class="sxs-lookup"><span data-stu-id="9c12c-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="9c12c-135">범주화된 기능을 생성하려면 다음 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="9c12c-136">열 시퀀스를 추가하여 숫자 열을 범주화합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-136">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="9c12c-137">범주화를 부울 변수 시퀀스로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-137">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="9c12c-138">마지막으로 더미 변수를 다시 원래 데이터 프레임에 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-138">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="9c12c-139"><a name="sql-featuregen"></a>다시 Azure blob에 데이터를 쓰고 Azure 기계 학습에서 데이터 사용</span><span class="sxs-lookup"><span data-stu-id="9c12c-139"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="9c12c-140">데이터를 탐색하고 필요한 기능을 만든 후에는 다음 단계에 따라 샘플링한 또는 기능화한 데이터를 Azure blob에 업로드하여 Azure 기계 학습에서 사용할 수 있습니다. Azure 기계 학습 스튜디오에서 추가 기능을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="9c12c-141">로컬 파일에 데이터 프레임을 씁니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-141">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="9c12c-142">다음과 같이 Azure blob에 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-142">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="9c12c-143">이제 아래 그림과 같이 Azure 기계 학습 [데이터 가져오기][import-data] 모듈을 사용하여 blob에서 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c12c-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span></span>

![판독기 blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

