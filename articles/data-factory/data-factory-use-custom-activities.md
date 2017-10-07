---
title: "Azure 데이터 팩터리 파이프라인에서 aaaUse 사용자 지정 활동"
description: "자세한 방법을 toocreate 사용자 지정 활동 Azure 데이터 팩터리 파이프라인에서 사용 하 고 있습니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>Azure Data Factory 파이프라인에서 사용자 지정 작업 사용

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 작업](data-factory-hive-activity.md) 
> * [Pig 작업](data-factory-pig-activity.md)
> * [MapReduce 작업](data-factory-map-reduce.md)
> * [Hadoop 스트리밍 작업](data-factory-hadoop-streaming-activity.md)
> * [Spark 작업](data-factory-spark.md)
> * [Machine Learning Batch 실행 작업](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 업데이트 리소스 작업](data-factory-azure-ml-update-resource-activity.md)
> * [저장 프로시저 작업](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 작업](data-factory-usql-activity.md)
> * [.NET 사용자 지정 작업](data-factory-use-custom-activities.md)

Azure Data Factory 파이프라인에서 사용할 수 있는 두 가지 작업 유형이 있습니다.

- [데이터 이동 작업](data-factory-data-movement-activities.md) 간에 toomove 데이터 [원본 및 싱크 데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다.
- [데이터 변환 작업](data-factory-data-transformation-activities.md) tootransform 데이터를 사용 하 여 Azure HDInsight, Azure 일괄 처리 및 Azure 기계 학습 등의 서비스를 계산 합니다. 

toomove 한 데이터를 Data Factory 지원 하지 않는 데이터 저장소에서 만들는 **사용자 지정 활동** 사용자 고유의 데이터 이동 논리 및 사용 하 여 hello의에서 활동과 파이프라인. 마찬가지로, 데이터 팩터리에서 지원 되지 않는 방식으로 데이터 tootransform/처리는 사용자 지정 활동 데이터 변환 논리로 만들고 파이프라인에서 hello 활동을 사용 합니다. 

사용자 지정 활동 toorun를 구성할 수 있습니다는 **Azure 배치** 풀의 가상 컴퓨터 또는 Windows 기반 **Azure HDInsight** 클러스터입니다. Azure Batch를 사용할 때는 기존 Azure Batch 풀만 사용할 수 있습니다. 반면, HDInsight를 사용할 때는 기존 HDInsight 클러스터 또는 필요 시 런타임에 자동으로 생성된 클러스터를 사용할 수 있습니다.  

hello 다음 연습에서는 사용자 지정.NET 작업 만들기 및 hello 사용자 지정 활동을 사용 하 여 파이프라인의 단계별 지침을 합니다. 사용 하 여 hello 연습은 **Azure 배치** 연결 된 서비스입니다. 대신 연결 된 서비스는 Azure HDInsight toouse, 형식의 연결 된 서비스를 만들면 **HDInsight** (HDInsight 클러스터 사용자 고유의) 또는 **HDInsightOnDemand** (데이터 팩터리에서 생성 하는 HDInsight 클러스터 요청 시)입니다. 그런 다음 사용자 지정 활동 toouse hello HDInsight 연결 된 서비스를 구성 합니다. 참조 [사용 하 여 Azure HDInsight 연결 된 서비스](#use-hdinsight-compute-service) Azure HDInsight toorun hello에 대 한 사용자 지정 활동을 사용 하 여 대 한 자세한 내용은 섹션.

> [!IMPORTANT]
> - 사용자 지정.NET 작업 hello Windows 기반 HDInsight 클러스터에 대해서만 실행 합니다. 이 제한에 대 한 해결 방법은 toouse hello Linux 기반 HDInsight 클러스터에서 맵 줄일 활동 toorun 사용자 지정 Java 코드입니다. 두 번째 방법은 toouse Vm toorun HDInsight 클러스터를 사용 하는 대신 사용자 지정 활동의 Azure 배치 풀 합니다.
> - 가능한 toouse 사용자 지정 활동 tooaccess 온-프레미스 데이터 원본에서 데이터 관리 게이트웨이 없습니다. 현재 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) Data Factory에 hello 복사 작업 및 저장된 프로시저 작업을 지원 합니다.   

## <a name="walkthrough-create-a-custom-activity"></a>연습: 사용자 지정 작업 만들기
### <a name="prerequisites"></a>필수 조건
* Visual Studio 2012/2013/2015
* [Azure .NET SDK](https://azure.microsoft.com/downloads/)

### <a name="azure-batch-prerequisites"></a>Azure 배치 필수 조건
Hello 연습에서는 Azure 배치를 계산 리소스로 사용 하 여 사용자 지정.NET 작업 실행. **Azure 배치** 는 대규모 병렬 실행에 대 한 서비스 및 고성능 컴퓨팅 hello 클라우드에서 효율적으로 (HPC) 응용 프로그램 플랫폼입니다. Azure 일괄 처리에서 관리 되는 계산 집약적인 작업 toorun 예약 **가상 컴퓨터의 컬렉션**를 계산할 수 있습니다 자동으로 크기 조정 작업의 리소스 toomeet hello 요구 하 고 있습니다. 참조 [Azure 배치 기본 사항] [ batch-technical-overview] hello Azure 배치 서비스의 문서에 대 한 자세한 개요입니다.

Hello 자습서에 대 한 Vm의 풀과 Azure 배치 계정을 만듭니다. Hello 단계는 다음과 같습니다.

1. 만들기는 **Azure 배치 계정** hello를 사용 하 여 [Azure 포털](http://portal.azure.com)합니다. 지침은 [Azure Batch 계정 만들기 및 관리][batch-create-account] 문서를 참조하세요.
2. Hello Azure 배치 계정 이름, 계정 키, URI 및 풀 이름 아래로 note 합니다. Azure 배치 연결 된 서비스 toocreate가 필요 합니다.
    1. Azure 배치 계정에 대 한 hello 홈 페이지에 표시 된 **URL** 형식에 따라 hello에: `https://myaccount.westus.batch.azure.com`합니다. 이 예제에서는 **myaccount** hello hello Azure 배치 계정 이름입니다. 연결 된 hello 서비스 정의에 사용할 URI은 hello 계정의 hello 이름 없이 hello URL입니다. 예: `https://<region>.batch.azure.com`
    2. 클릭 **키** hello 왼쪽된 메뉴 및 복사 hello **기본 액세스 키**합니다.
    3. 기존 풀 toouse 클릭 **풀** hello 메뉴 및 hello 적어 둡니다 **ID** hello 풀의 합니다. 기존 풀 없으면 toohello 다음 단계로 이동 합니다.     
2. **Azure 배치 풀**을 만듭니다.

   1. Hello에 [Azure 포털](https://portal.azure.com), 클릭 **찾아보기** 에서 왼쪽된 메뉴 hello 하 고 클릭 **일괄 처리 계정**합니다.
   2. 선택 하면 Azure 배치 계정 tooopen hello **일괄 처리 계정** 블레이드입니다.
   3. **풀** 타일을 클릭합니다.
   4. Hello에 **풀** 블레이드에서 hello 도구 모음 tooadd 풀에 추가 단추를 클릭 합니다.
      1. Hello 풀 (풀 ID)에 대 한 ID를 입력 합니다. 참고 hello **hello 풀의 ID**; hello Data Factory 솔루션을 만들 때 필요 합니다.
      2. 지정 **Windows Server 2012 R2** hello 운영 체제 제품군 설정에 대 한 합니다.
      3. **노드 가격 책정 계층**을 선택합니다.
      4. 입력 **2** hello에 대 한 값으로 **대상 전용** 설정 합니다.
      5. 입력 **2** hello에 대 한 값으로 **노드당 최대 작업** 설정 합니다.
   5. 클릭 **확인** toocreate hello 풀입니다.
   6. Hello 기록해 **ID** hello 풀의 합니다. 



### <a name="high-level-steps"></a>대략적인 단계
이 연습의 일부분으로 수행 hello 두 개의 상위 수준 단계는 다음과 같습니다. 

1. 간단한 데이터 변환/처리 논리가 포함된 사용자 지정 작업을 만듭니다.
2. Hello 사용자 지정 활동을 사용 하는 파이프라인을 Azure 데이터 팩터리를 만듭니다.

### <a name="create-a-custom-activity"></a>사용자 지정 작업 만들기
toocreate.NET 사용자 지정 활동을 만듭니다는 **.NET 클래스 라이브러리** 를 구현 하는 클래스를 사용 하 여 프로젝트 **IDotNetActivity** 인터페이스입니다. 이 인터페이스는 [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) 라는 메서드 하나만 포함하며 서명은 다음과 같습니다.

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


hello 메서드 4 개의 매개 변수를 사용 합니다.

- **linkedServices**. 이 속성은 hello 활동에 대 한 입/출력 데이터 집합에서 참조 하는 데이터 저장소 연결 된 서비스의 열거형 목록.   
- **datasets**. 이 속성은 hello 활동에 대 한 입/출력 데이터 집합의 열거형 목록. 이 매개 변수 tooget hello 위치 및 입력 및 출력 데이터 집합에 정의 된 스키마를 사용할 수 있습니다.
- **activity**. 이 속성은 hello 현재 활동을 나타냅니다. 사용자 지정 활동 hello와 연관 된 확장 속성 사용된 tooaccess 수 있습니다. 자세한 내용은 [확장 속성 액세스](#access-extended-properties)를 참조하세요.
- **logger**. 이 개체를 사용 하면 디버그 주석을 해당 화면 hello 파이프라인에 대 한 hello 사용자 로그에 기록할 수 있습니다.

hello 메서드 hello 미래에 함께 사용 되는 toochain 사용자 지정 활동을 저장할 수 있는 사전을 반환 합니다. 이 기능은 아직 구현 되지 않았습니다, 그리고 따라서 hello 메서드에서 빈 사전이 반환을 반환 합니다.  

### <a name="procedure"></a>절차
1. **.NET 클래스 라이브러리** 프로젝트를 만듭니다.
   <ol type="a">
     <li><b>Visual Studio 2017</b> 또는 <b>Visual Studio 2015</b> 또는 <b>Visual Studio 2013</b> 또는 <b>Visual Studio 2012</b>를 시작합니다.</li>
     <li>클릭 <b>파일</b>, 너무 가리킨<b>새로</b>를 클릭 하 고 <b>프로젝트</b>합니다.</li>
     <li><b>템플릿</b>을 확장하고 <b>Visual C#</b>를 선택합니다. 이 연습에서는 C#을 사용 하지만 모든.NET 언어 toodevelop hello 사용자 지정 활동을 사용할 수 있습니다.</li>
     <li>선택 <b>클래스 라이브러리</b> hello hello 오른쪽에 프로젝트 형식 목록에서 합니다. VS 2017에서 <b>클래스 라이브러리(.NET Framework)</b> 를 선택합니다.</li>
     <li>입력 <b>MyDotNetActivity</b> hello에 대 한 <b>이름</b>합니다.</li>
     <li>선택 <b>C:\ADFGetStarted</b> hello에 대 한 <b>위치</b>합니다.</li>
     <li>클릭 <b>확인</b> toocreate hello 프로젝트.</li>
   </ol>
2.클릭 **도구**, 너무 가리킨**NuGet 패키지 관리자**를 클릭 하 고 **패키지 관리자 콘솔**합니다.
3. Hello 패키지 관리자 콘솔에서에서 실행 하 여 다음 명령 tooimport hello **Microsoft.Azure.Management.DataFactories**합니다.

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. 가져오기 hello **Azure 저장소** toohello 프로젝트에서 NuGet 패키지 합니다.

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > 데이터 팩터리 서비스 시작 관리자에는 특히 WindowsAzure.Storage hello 4.3 버전이 필요합니다. 참조 tooa를 추가 하는 경우 사용자 지정 작업 프로젝트에 Azure 저장소 어셈블리의 이후 버전 hello 활동에서 실행 오류가 표시 됩니다. tooresolve hello 오류 참조 [Appdomain 격리](#appdomain-isolation) 섹션. 
5. Hello 다음 추가 **를 사용 하 여** hello 프로젝트에서 문 toohello 소스 파일입니다.

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Hello의 hello 이름 변경 **네임 스페이스** 너무**MyDotNetActivityNS**합니다.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Hello 클래스의 hello 이름도 변경**MyDotNetActivity** hello에서 파생 되 고 **IDotNetActivity** hello 다음 코드 조각에에서 나와 있는 것 처럼 인터페이스:

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. 구현 (추가) hello **Execute** hello 방식의 **IDotNetActivity** toohello 인터페이스 **MyDotNetActivity** 다음 샘플 코드 toohello 메서드에 클래스와 복사 hello 합니다.

    hello 다음 샘플 수를 hello hello 검색 단어 ("Microsoft")의 발생 수는 데이터 조각과와 연결 된 각 blob 합니다.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. Hello 다음 도우미 메서드를 추가 합니다. 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    hello GetFolderPath 메서드 반환 hello 경로 toohello 폴더를 데이터 집합을 hello tooand hello GetFileName 메서드 반환 hello hello blob 파일의 이름을/데이터 집합 가리키는 hello를 가리킵니다. HavefolderPath 있습니다 {Year} 같은 변수를 사용 하 여 정의 하는 경우 {Month} {Day} 등, hello 메서드 반환 값이 런타임 바꾸지 않고 그대로 문자열 hello 합니다. SliceStart, SliceEnd 등에 대한 액세스에 대해 자세히 알아보려면 [확장 속성 액세스](#access-extended-properties) 를 참조하세요.    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    hello Calculate 메서드 hello 키워드 hello 입력된 파일 (blob의 hello 폴더에 있는 경우)에서 Microsoft의 인스턴스 수를 계산합니다. hello 검색 단어 ("Microsoft") hello 코드에 하드 코딩 되어 있습니다.
10. Hello 프로젝트를 컴파일하십시오. 클릭 **빌드** hello 메뉴에서 **솔루션 빌드**합니다.

    > [!IMPORTANT]
    > 프로젝트에 대 한 hello 대상 프레임 워크로.NET Framework의 집합 4.5.2 버전: hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성** tooset hello에 대 한 대상 프레임 워크입니다. 데이터 팩터리는 .NET Framework 4.5.2 이후 버전에 대해 컴파일된 사용자 지정 작업을 지원하지 않습니다.

11. 시작 **Windows 탐색기**, 너무 이동**bin\debug** 또는 **bin\release** 빌드의 hello 종류에 따라 폴더입니다.
12. Zip 파일을 만들 **MyDotNetActivity.zip** hello에서 모든 hello 이진 파일을 포함 하는 <project folder>\bin\Debug 폴더입니다. Hello 포함 **MyDotNetActivity.pdb** 파일 오류가 발생 한 경우 hello 문제를 발생 시킨 hello 소스 코드의 줄 번호 등의 추가 정보를 받을 수 있도록 합니다. 

    > [!IMPORTANT]
    > Hello에 hello 사용자 지정 활동 이어야 hello zip 파일의 파일을 hello 모든 **최상위** 와 하위 폴더가 없습니다.

    ![이진 출력 파일](./media/data-factory-use-custom-activities/Binaries.png)
14. 명명된 Blob 컨테이너 **customactivitycontainer**가 아직 없는 경우 새로 만듭니다. 
15. MyDotNetActivity.zip에 blob toohello customactivitycontainer로 업로드 하는 **범용** AzureStorageLinkedService에서 참조는 Azure blob 저장소 (Blob storage 하지 핫/쿨).  

> [!IMPORTANT]
> Data Factory 프로젝트를 포함 하는 Visual Studio에서이.NET 활동 프로젝트 tooa 솔루션을 추가 하 고 hello Data Factory 응용 프로그램 프로젝트에서 참조 too.NET 활동 프로젝트를 추가 하는 경우 수동으로 만드는 tooperform hello 마지막 두 단계 불필요 hello zip 파일을 선택 하 고 toohello 범용 Azure blob 저장소에 업로드 합니다. Visual Studio를 사용 하 여 데이터 팩터리 엔터티를 게시 하면 다음이 단계 hello 게시 프로세스에 의해 자동으로 수행 됩니다. 자세한 내용은 [Visual Studio의 데이터 팩터리 프로젝트](#data-factory-project-in-visual-studio) 섹션을 참조하세요.

## <a name="create-a-pipeline-with-custom-activity"></a>사용자 지정 작업을 포함하는 파이프라인 만들기
사용자 지정 활동을 만들고 바이너리 tooa blob 컨테이너에서 hello zip 파일을 업로드 한 **범용** Azure 저장소 계정입니다. 이 섹션에서는 Azure 데이터 팩터리에 hello 사용자 지정 활동을 사용 하는 파이프라인을 사용 하 여 만듭니다.

hello 사용자 지정 활동에 대 한 입력된 데이터 집합 hello hello blob 저장소의 adftutorial 컨테이너의 hello customactivityinput 폴더에 blob을 (파일)을 나타냅니다. hello 활동에 대 한 출력 데이터 집합 hello hello blob 저장소의 adftutorial 컨테이너의 hello customactivityoutput 폴더에 출력 blob을 나타냅니다.

만들 **file.txt** 다음 콘텐츠을 너무 업로드 hello로 파일**customactivityinput** hello의 폴더 **adftutorial** 컨테이너입니다. 이미 존재 하지 않는 경우 hello adftutorial 컨테이너를 만듭니다. 

```
test custom activity Microsoft test custom activity Microsoft
```

hello 입력된 폴더 hello 폴더에 파일이 두 개 이상의 경우에 Azure 데이터 팩터리에서 조각 tooa 해당 합니다. 각 조각은 hello 파이프라인에서 처리 될 때 hello 사용자 지정 활동에 대 한 해당 조각의 hello 입력된 폴더의 모든 hello blob을 반복 합니다.

하나 이상의 줄만 작성 (hello 입력된 폴더에 있는 blob 수와 동일) hello adftutorial\customactivityoutput 폴더에 파일을 출력 하는 것이 표시 됩니다.

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


이 섹션에서 수행 하는 hello 단계는 다음과 같습니다.

1. **데이터 팩터리**를 만듭니다.
2. 만들 **연결 된 서비스** Vm는 hello에 사용자 지정 활동을 실행 하 고 hello hello 입/출력 blob를 보유 하는 Azure 저장소의 hello Azure 배치 풀에 대 한 합니다.
3. 입력 및 출력 만들기 **데이터 집합** hello 사용자 지정 활동의 입력 및 출력을 나타냅니다.
4. 만들기는 **파이프라인** hello 사용자 지정 활동을 사용 하 여 합니다.

> [!NOTE]
> Hello 만들기 **file.txt** 아직 수행 하지 않은 경우 blob 컨테이너 tooa을 업로드 합니다. Hello 이전 섹션의에서 지침을 참조 하십시오.   

### <a name="step-1-create-hello-data-factory"></a>1 단계: hello 데이터 팩터리 만들기
1. 로그인 한 후 toohello Azure 포털 수행 hello 단계를 수행 합니다.
   1. 클릭 **새로** hello 왼쪽된 메뉴에 있습니다.
   2. 클릭 **데이터 + 분석** hello에 **새로** 블레이드입니다.
   3. 클릭 **Data Factory** hello에 **데이터 분석** 블레이드입니다.
   
    ![새 Azure Data Factory 메뉴](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. Hello에 **새 데이터 팩터리** 블레이드에서 입력 **CustomActivityFactory** hello 이름에 대 한 합니다. hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다. Hello 오류가 나타나면: **"CustomActivityFactory" 데이터 팩터리 이름을 사용할 수 없으면**, hello 데이터 팩터리의 hello 이름 변경 (예를 들어 **yournameCustomActivityFactory**) 만들기를 시도 하십시오. 다시 실행 합니다.

    ![새 Azure Data Factory 블레이드](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. **리소스 그룹 이름**을 클릭하여 기존 리소스 그룹을 선택하거나 리소스 그룹을 만듭니다.
4. 올바른 hello를 사용 하 고 있는지 확인 하십시오. **구독** 및 **지역** hello 데이터 팩터리 toobe 만든 원하는 합니다.
5. 클릭 **만들기** hello에 **새 데이터 팩터리** 블레이드입니다.
6. Hello에 생성 되 고 hello 데이터 팩터리 참조 **대시보드** hello Azure 포털의.
7. Hello Data Factory 블레이드 보여 주는 참조 hello 데이터 팩터리에서 만들어진 후에 성공적으로, hello 데이터 팩터리의 내용을 hello 합니다.
    
    ![데이터 팩터리 블레이드](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>2단계: 연결된 서비스 만들기
연결 된 서비스 데이터 저장소를 연결 하거나 서비스 tooan Azure 데이터 팩터리를 계산 합니다. 이 단계에서는 Azure 저장소 계정 및 Azure 배치 계정 tooyour 데이터 팩터리를 연결합니다.

#### <a name="create-azure-storage-linked-service"></a>Azure 저장소 연결된 서비스 만들기
1. Hello 클릭 **작성자 및 배포** hello 타일 **DATA FACTORY** 블레이드 **CustomActivityFactory**합니다. 데이터 팩터리 편집기 hello를 표시 됩니다.
2. 클릭 **새 데이터 저장소** 명령 모음 hello 되 고 선택 **Azure 저장소**합니다. 표시 되어야 hello Azure 저장소를 만들기 위한 JSON 스크립트 hello 편집기에서 서비스를 연결 합니다.
    
    ![새 데이터 저장소 - Azure Storage](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. 대체 `<accountname>` 사용자의 Azure 저장소 계정 이름의 및 `<accountkey>` 의 hello Azure 저장소 계정 액세스 키로 합니다. toolearn 어떻게 tooget 저장소 액세스 키가 참조 [보기, 복사 및 다시 생성 저장소 액세스 키](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.

    ![Azure Storage 연결 서비스](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. 클릭 **배포** hello 명령 toodeploy hello 연결 된 서비스 모음에 있습니다.

#### <a name="create-azure-batch-linked-service"></a>Azure 배치 연결된 서비스 만들기
1. 데이터 팩터리 편집기 hello 클릭 **중... 더 많은** hello 명령 모음에서 **새 계산**를 선택한 후 **Azure 배치** hello 메뉴에서 합니다.

    ![새 계산 - Azure 배치](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. Hello 다음 변경 내용을 toohello JSON 스크립트를 확인 합니다.

   1. Hello에 대 한 Azure 배치 계정 이름을 지정 **accountName** 속성입니다. hello **URL** hello에서 **Azure 배치 계정 블레이드** 형식에 따라 hello에: `http://accountname.region.batch.azure.com`합니다. Hello에 대 한 **batchUri** 속성에 hello JSON, tooremove 필요한 `accountname.` hello URL과 사용 하 여 hello에서 `accountname` hello에 대 한 `accountName` JSON 속성입니다.
   2. Hello에 대 한 hello Azure 배치 계정 키를 지정 **accessKey** 속성입니다.
   3. 만든 hello 풀의 hello 이름을 hello에 대 한 필수 구성 요소의 일부분으로 지정 **poolName** 속성입니다. Hello 풀의 hello 이름 대신 hello 풀의 hello ID를 지정할 수 있습니다.
   4. Hello에 대 한 Azure 일괄 처리 URI를 지정 **batchUri** 속성입니다. 예: `https://westus.batch.azure.com`.  
   5. Hello 지정 **AzureStorageLinkedService** hello에 대 한 **linkedServiceName** 속성입니다.

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Hello에 대 한 **poolName** 속성을 hello 풀의 hello 이름 대신 hello 풀의 hello ID를 지정할 수도 있습니다.

      > [!IMPORTANT]
      > HDInsight에 대해서와 마찬가지로 hello Data Factory 서비스가 Azure 일괄 처리에 대 한 주문형 옵션을 지원 하지 않습니다. Azure Data Factory에서는 사용자 고유의 Azure Batch 풀만 사용할 수 있습니다.   
    

### <a name="step-3-create-datasets"></a>3단계: 데이터 집합 만들기
이 단계에서는 toorepresent 입력 데이터 집합 만들기 및 데이터를 출력 합니다.

#### <a name="create-input-dataset"></a>입력 데이터 집합 만들기
1. Hello에 **편집기** hello Data Factory에 대 한 클릭 **중... 더 많은** hello 명령 모음에서 **새 데이터 집합**를 선택한 후 **Azure Blob 저장소** hello 드롭 다운 메뉴에서 합니다.
2. Hello를 JSON hello 오른쪽 창에서 다음 JSON 코드 조각은 hello로 바꿉니다.

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   이 연습에서는 시작 시간: 2016-11-16T00:00:00Z 및 종료 시간: 2016-11-16T05:00:00Z로 나중에 파이프라인을 만듭니다. 것 이므로 예약 된 tooproduce 데이터 매시간는 5 개의 입/출력 분할 영역 (사이 **00**: 00:00-> **05**: 00:00).

   hello **주파수** 및 **간격** hello 입력된 데이터 집합 너무 설정 되어**시간** 및 **1**, 즉, 해당 hello 조각 ´ ï ´ 입력 매시간 합니다. 이 샘플에서는 동일한 hello는 hello intputfolder에서 파일 (file.txt).

   다음은 JSON 코드 조각은 위에 hello에서 시스템 변수 SliceStart로 표시 된 각 조각에 대 한 hello 시작 시간입니다.
3. 클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **InputDataset**합니다. Hello 표시 되는지 확인 **테이블 만든 성공적으로** hello 편집기의 hello 제목 표시줄에 메시지가 있습니다.

#### <a name="create-an-output-dataset"></a>출력 데이터 집합 만들기
1. Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은** hello 명령 모음에서 **새 데이터 집합**를 선택한 후 **Azure Blob 저장소**합니다.
2. 다음 JSON 스크립트 hello hello 오른쪽 창에서 hello JSON 스크립트를 바꿉니다.

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     출력 위치는 **adftutorial/customactivityoutput/** 및 출력 파일 이름은 여기서 yyyy MM-dd HH는 hello 연도, 월, 날짜 및 시간 생성 hello 조각의 MM dd HH.txt yyyy입니다. 자세한 내용은 [개발자 참조][adf-developer-reference](영문)를 참조하세요.

    각 입력 조각에 대해 출력 BLOB/파일이 생성됩니다. 각 조각에 대해 출력 파일의 이름을 지정하는 방법은 다음과 같습니다. 하나의 출력 폴더에 모든 hello 출력 파일이 생성 됩니다: **adftutorial\customactivityoutput**합니다.

   | 조각 | 시작 시간 | 출력 파일 |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    입력된 폴더에 모든 hello 파일 위에서 언급 한 hello 시작 시간 조각에 포함 되어 있는지를 기억 합니다. 이 조각이 처리 되 면 hello 사용자 지정 활동 각 파일을 통해 검색 하 고 hello 검색 단어 ("Microsoft")의 발생 수와 hello 출력 파일의 줄을 생성 합니다. 각 시간 조각에 대 한 hello 출력 파일에 세 줄은 hello inputfolder에 세 개의 파일이 있는 경우: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, 등입니다.
3. toodeploy hello **OutputDataset**, 클릭 **배포** hello 명령 모음에서 합니다.

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>만들기 및 hello 사용자 지정 활동을 사용 하는 파이프라인 실행
1. 데이터 팩터리 편집기 hello 클릭 **중... 더 많은**를 선택한 후 **새 파이프라인** hello 명령 모음에서 합니다. 
2. Hello를 JSON hello 오른쪽 창에서 다음 JSON 스크립트 hello 바꿉니다.

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    포인트 다음 참고 hello:

   * **동시성** 너무 설정**2** 두 슬라이스 hello Azure 배치 풀에 2 개의 Vm에서 동시에 처리할 수 있도록 합니다.
   * Hello 활동 섹션에서 하나의 활동 활동이 며 유형은: **DotNetActivity**합니다.
   * **AssemblyName** 설정 않으면 hello DLL의 toohello 이름이: **MyDotnetActivity.dll**합니다.
   * **EntryPoint** 너무 설정**MyDotNetActivityNS.MyDotNetActivity**합니다.
   * **PackageLinkedService** 너무 설정**AzureStorageLinkedService** hello 사용자 지정 활동 zip 파일이 포함 된 toohello blob 저장소를 가리키는 합니다. 사용 하는 경우 서로 다른 Azure 저장소 계정에 대 한 입/출력 파일 하 고 hello zip 파일을 사용자 지정 활동을 만들면 다른 Azure 저장소 연결 된 서비스입니다. 이 문서에서는 사용 한다고 가정 hello Azure 저장소 계정과 동일한 계정입니다.
   * **PackageFile** 너무 설정**customactivitycontainer/MyDotNetActivity.zip**합니다. Hello 형식: containerforthezip/nameofthezip.zip 합니다.
   * hello 사용자 지정 활동은 **InputDataset** 입력으로 및 **OutputDataset** 출력으로 합니다.
   * hello 사용자 지정 활동의 hello linkedServiceName 속성 가리킵니다 toohello **AzureBatchLinkedService**, 일괄 처리는 Azure Vm에서 toorun 필요한 Azure Data Factory 해당 hello 사용자 지정 활동 지시 합니다.
   * **isPaused** 너무 속성이**false** 기본적으로 합니다. hello 파이프라인 hello 지난 hello 조각 시작 때문에이 예에서 즉시 실행 합니다. 이 속성 tootrue toopause hello 파이프라인을 설정 하 고 뒤로 toofalse toorestart를 설정할 수 있습니다.
   * hello **시작** 시간 및 **끝** 시간은 **5** 더 많이 떨어져 있는 시간 및 분할 영역 생성 된 매시간, 되므로 5 개 조각 hello 파이프라인에 의해 생성 됩니다.
3. toodeploy hello 파이프라인 클릭 **배포** hello 명령 모음에서 합니다.

### <a name="monitor-hello-pipeline"></a>모니터 hello 파이프라인
1. Data Factory 블레이드에서 hello hello Azure 포털에서에서 클릭 **다이어그램**합니다.

    ![다이어그램 타일](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. 다이어그램 보기 hello에서 이제 OutputDataset hello를 클릭 합니다.

    ![다이어그램 뷰](./media/data-factory-use-custom-activities/diagram.png)
3. Hello 5 개의 출력 조각만 hello 준비 상태에 있는지 표시 됩니다. Hello 준비 상태에 있지 않기 경우 아직 생성 된 하지 않았습니다. 

   ![출력 분할](./media/data-factory-use-custom-activities/OutputSlices.png)
4. Hello blob 저장소에 hello hello 출력 파일이 생성 되는 확인 **adftutorial** 컨테이너입니다.

   ![사용자 지정 작업의 출력][image-data-factory-ouput-from-custom-activity]
5. Hello 출력 파일을 열면 hello 출력 출력에 따라 유사한 toohello 나타납니다.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. 사용 하 여 hello [Azure 포털] [ azure-preview-portal] 또는 Azure PowerShell cmdlet toomonitor 데이터 팩터리, 파이프라인 및 데이터 집합입니다. Hello 메시지를 볼 수 **ActivityLogger** hello hello 포털 또는 cmdlet을 사용 하 여 다운로드할 수 있는 hello 로그 (특히 사용자 0.log)에 사용자 지정 활동에 대 한 hello 코드입니다.

   ![사용자 지정 작업의 로그 다운로드][image-data-factory-download-logs-from-custom-activity]

데이터 집합 및 파이프라인 모니터링에 대한 자세한 단계는 [파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 를 참조하세요.      

## <a name="data-factory-project-in-visual-studio"></a>Visual Studio의 데이터 팩터리 프로젝트  
Azure Portal 대신 Visual Studio를 사용하여 데이터 팩터리 엔터티를 만들고 게시할 수 있습니다. 자세한 만들기에 대 한 정보를 Visual Studio를 사용 하 여 데이터 팩터리 엔터티를 게시, 참조에 대 한 [Visual Studio를 사용 하 여 첫 번째 파이프라인 빌드](data-factory-build-your-first-pipeline-using-vs.md) 및 [Azure Blob tooAzure SQL에서에서 데이터를 복사](data-factory-copy-activity-tutorial-using-visual-studio.md) 문서입니다.

Visual Studio에서 데이터 팩터리 프로젝트를 만들면 다음 추가 단계를 hello 수행:
 
1. Hello Data Factory 프로젝트 toohello hello 사용자 지정 활동 프로젝트를 포함 하는 Visual Studio 솔루션을 추가 합니다. 
2. Hello Data Factory 프로젝트에서 참조 toohello.NET 활동 프로젝트를 추가 합니다. 데이터 팩터리 프로젝트를 마우스 오른쪽 단추로 클릭, 너무 가리킨**추가**, 클릭 하 고 **참조**합니다. 
3. Hello에 **참조 추가** 대화 상자, 선택 hello **MyDotNetActivity** 프로젝트를 마우스 클릭 **확인**합니다.
4. 빌드하고 hello 솔루션을 게시 합니다.

    > [!IMPORTANT]
    > 데이터 팩터리 엔터티를 게시 하는 경우 zip 파일을 자동으로 만들어집니다 이며 toohello 업로드 된 blob 컨테이너: customactivitycontainer 합니다. Hello blob 컨테이너가 없는 경우 자동으로 만들어집니다 너무 합니다.  


## <a name="data-factory-and-batch-integration"></a>Data Factory 및 배치 통합
데이터 팩터리 서비스 hello hello 이름의 Azure 일괄 처리에서 작업을 만듭니다: **adf poolname: 작업 xxx**합니다. 클릭 **작업** hello 왼쪽된 메뉴에서 합니다. 

![Azure Data Factory - 배치 작업](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

조각의 각 작업 실행에 대한 작업(task)이 만들어집니다. 처리는 5 개의 분할 영역 준비 toobe가 없을 경우이 작업의 5 개 작업이 만들어집니다. Hello 배치 풀에에서 여러 계산 노드 있는 경우 두 개 이상의 분할 영역 병렬로 실행할 수 있습니다. 당 최대 작업 수 hello 계산 노드가 설정 될 경우 너무 > 1, 할 수도 있습니다 hello에서 실행 중인 둘 이상의 슬라이스 동일한 계산 합니다.

![Azure Data Factory - 배치 작업 태스크](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

다이어그램을 다음 hello Azure 데이터 팩터리 및 일괄 처리 작업 간의 hello 관계를 보여 줍니다.

![데이터 팩터리 및 배치](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>오류 문제 해결
문제 해결은 몇 가지 기본적인 방법으로 구성됩니다.

1. Hello 다음 오류가 표시 되는 경우 범용 Azure blob 저장소를 사용 하는 대신 핫/쿨 blob 저장소를 사용 하 될 수 있습니다. Hello zip 파일 tooa 업로드 **범용 Azure 저장소 계정**합니다. 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. Hello 다음 오류가 표시 되 면 확인 hello에 대 한 지정한 hello CS 파일 일치 hello 이름에서 hello 클래스의 해당 hello 이름을 **EntryPoint** hello 파이프라인 JSON의 속성입니다. Hello 연습 hello 클래스의 이름을: MyDotNetActivity, 및 JSON hello에 EntryPoint hello: MyDotNetActivityNS 합니다. **MyDotNetActivity**합니다.

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   Hello 이름이 일치 하는 경우에 있는지 확인 모든 hello 바이너리 hello **루트 폴더** hello zip 파일의 합니다. 즉, hello zip 파일을 열 때는 hello 루트 폴더에, 모든 하위 폴더에 없는 모든 hello 파일에 표시 됩니다.   
3. Hello 입력된 조각이 너무 설정 되어 있지 않으면**준비**, hello 입력된 폴더 구조가 올바른지 확인 하 고 **file.txt** hello 입력된 폴더에 있습니다.
3. Hello에 **Execute** 사용자 지정 활동을 사용 하 여 hello 방식의 **IActivityLogger** 때 도움이 되는 개체 toolog 정보 문제를 해결 합니다. hello 사용자 로그 파일에 기록 하는 hello 메시지 표시 (명명 된 하나 이상의 파일: 0.log 사용자, 사용자 1.log, 사용자 2.log 등.).

   Hello에 **OutputDataset** 블레이드에서 hello 조각 toosee hello 클릭 **데이터 조각을** 블레이드 해당 조각에 대 한 합니다. 해당 조각에 대한 **작업 실행** 이 표시됩니다. Hello 조각에 대 한 실행 하는 하나의 활동이 표시 됩니다. Hello에 대 한 실행 하는 다른 작업을 시작할 수 hello 명령 모음에서 실행을 클릭 하면 동일한 분할 영역입니다.

   Hello hello 작업 실행을 클릭할 때 표시 **작업 실행 세부 정보** 블레이드 로그 파일의 목록과 함께 합니다. Hello user_0.log 파일에 기록 된 메시지를 참조 하십시오. 오류가 발생 하면 hello 재시도 횟수는 hello 파이프라인/활동 JSON에서에서 too3 설정 되어 있으므로 세 가지 활동을 실행 표시 됩니다. Hello 작업 실행을 클릭 하면 tootroubleshoot hello 오류를 검토할 수 있도록 하는 hello 로그 파일이 표시 됩니다.

   로그 파일의 hello 목록에서 클릭 hello **사용자 0.log**합니다. Hello 오른쪽 패널에서 결과인 hello hello를 사용 하 여 **IActivityLogger.Write** 메서드. 일부 메시지가 보이지 않으면 user_1.log, user_2.log 등 비슷한 이름의 로그 파일이 더 있는지 확인합니다. 그렇지 않으면 hello 메시지를 마지막 로그온 한 후 hello 코드 되지 않았습니다.

   또한 **system-0.log**에서 시스템 오류 메시지 및 예외를 확인합니다.
4. Hello 포함 **PDB** hello 오류 세부 정보와 같은 정보를 포함할 수 있도록 hello zip 파일에 파일 **호출 스택을** 오류가 발생할 경우.
5. Hello에 hello 사용자 지정 활동 이어야 hello zip 파일의 파일을 hello 모든 **최상위** 와 하위 폴더가 없습니다.
6. 해당 hello 확인 **assemblyName** (MyDotNetActivity.dll) **entryPoint**(MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) 및 **packageLinkedService** (toohello 가리켜야 **범용**hello zip 파일을 포함 하는 Azure blob 저장소) toocorrect 값 설정 됩니다.
7. 오류 및 원하는 tooreprocess hello 슬라이스를 수정한 경우 hello hello 조각 마우스 오른쪽 단추로 클릭 **OutputDataset** 블레이드에 대 한 클릭 **실행**합니다.
8. Hello 다음 오류가 표시 되 면 버전 > 4.3.0의 hello Azure 저장소 패키지를 사용 하는 합니다. 데이터 팩터리 서비스 시작 관리자에는 특히 WindowsAzure.Storage hello 4.3 버전이 필요합니다. 참조 [Appdomain 격리](#appdomain-isolation) hello를 사용 해야 할 경우 해결에 대 한 섹션 Azure 저장소 어셈블리의 이후 버전입니다. 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    Azure 저장소 패키지의 버전 4.3.0 hello를 사용 하려면 hello 참조 tooAzure 저장소의 기존 패키지 버전 > 4.3.0를 제거 합니다. 그런 다음 hello NuGet 패키지 관리자 콘솔에서 다음 명령을 실행 합니다. 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    Hello 프로젝트를 빌드하십시오. Hello bin\Debug 폴더에서 버전 > 4.3.0의 Azure.Storage 어셈블리를 삭제 합니다. Zip 파일을 이진 파일 및 hello PDB 파일을 만듭니다. (Customactivitycontainer) hello blob 컨테이너에서이 hello 이전 zip 파일을 바꿉니다. 다시 실행 hello에 실패 한 조각이 (분할 영역을 마우스 오른쪽 단추로 클릭 하 고 실행을 차례로 클릭).   
8. 사용자 지정 활동 hello hello를 사용 하지 않는 **app.config** 패키지에서 파일입니다. 따라서 코드 hello 구성 파일에서 모든 연결 문자열에 읽기, 하는 경우 런타임 시 작동 하지 않습니다. hello 모범 사례 toohold Azure 일괄 처리를 사용 하는 경우의 모든 암호는 **Azure KeyVault**, 인증서 기반 서비스 보안 주체 tooprotect hello를 사용 하 여 **keyvault**, hello 인증서 배포 tooAzure 배치 풀 합니다. .NET 사용자 지정 활동을 hello 다음 런타임에 KeyVault hello에서 비밀 정보에 액세스할 수 있습니다. 이 솔루션은 일반 솔루션 및 tooany 유형의 암호 뿐 아니라 연결 문자열을 확장할 수 있습니다.

   보다 쉽게 해결 (있지만 최상의 방법은 아님): 만들 수는 **Azure SQL 연결 된 서비스** 를 위해 연결 문자열 설정을 사용 하 여 hello 연결 된 서비스 및 더미 입력된 데이터 집합으로 체인 hello 데이터 집합을 데이터 집합 만들기 toohello 사용자 지정.NET 작업입니다. 액세스 hello hello 사용자 지정 활동 코드에서 서비스의 연결 문자열을 연결 하는 다음 할 수 있습니다.  

## <a name="update-custom-activity"></a>사용자 지정 작업 업데이트
Hello 사용자 지정 활동에 대 한 hello 코드를 업데이트 하는 경우 빌드하고 새 바이너리 toohello blob 저장소를 포함 하는 hello zip 파일을 업로드 합니다.

## <a name="appdomain-isolation"></a>Appdomain 격리
참조 [크로스 AppDomain 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) toocreate 하지 않은 사용자 지정 활동 tooassembly 버전 hello 데이터 팩터리 시작 관리자에서 사용을 제한 하는 방법을 보여 주는 (예: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x 등.).

## <a name="access-extended-properties"></a>확장 속성 액세스
다음 예제는 hello와 같이 hello 활동 JSON에에서 확장된 속성을 선언할 수 있습니다.

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


Hello 예제에서는 두 가지 확장된 속성: **SliceStart** 및 **DataFactoryName**합니다. SliceStart에 대 한 hello 값 hello SliceStart 시스템 변수를 기반으로 합니다. 지원되는 시스템 변수 목록은 [시스템 변수](data-factory-functions-variables.md) 를 참조하세요. DataFactoryName hello 값은 하드 코딩 된 tooCustomActivityFactory입니다.

속성 hello에 이러한 확장 tooaccess **Execute** 메서드를 사용 하 여 코드와 유사한 toohello 코드 다음:

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Azure Batch의 자동 확장
**자동 크기 조정** 기능으로 Azure 배치 풀을 만들 수 있습니다. 예를 들어 0 전용된 Vm 및 보류 중인 작업 수가 hello 기반으로 하는 자동 크기 조정 수식을 사용 하 여 azure 배치 풀을 만들 수 있습니다. 

hello 수식 여기에 동작을 수행 하는 hello 달성: hello 풀 처음 만들어질 때 1 VM으로 시작 합니다. $PendingTasks 메트릭을 실행 + 활성 (대기) hello 다양 한 작업 정의 상태입니다.  hello 수식은 지난 180 초 동안 hello에 보류 중인 작업의 hello 평균 숫자를 검색 하 고 TargetDedicated를 적절 하 게 설정 합니다. 또한 TargetDedicated가 25개의 VM을 초과하지 않도록 합니다. 따라서 새 작업이 제출 되는 대로 풀에서 자동으로 증가 및 완료 작업으로 Vm 하나씩 무료 해지고 해당 Vm을 축소 하는 hello 자동 크기 조정. startingNumberOfVMs 및 maxNumberofVMs 조정된 tooyour 요구 될 수 있습니다.

자동 크기 조정 수식:

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

자세한 내용은 [Azure 배치 풀에서 자동으로 계산 노드 크기 조정](../batch/batch-automatic-scaling.md) 을 참조하세요.

Hello 풀 hello 기본값을 사용 하는 경우 [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello 일괄 처리 서비스는 hello 사용자 지정 활동을 실행 하기 전에 tooprepare hello VM 15-30 분 걸릴 수 있습니다.  Hello 풀 다른 autoScaleEvaluationInterval를 사용 하는 경우 일괄 처리 서비스 hello autoScaleEvaluationInterval + 10 분 걸릴 수 있습니다.

## <a name="use-hdinsight-compute-service"></a>HDInsight 계산 서비스 사용
Hello 연습에서는 Azure 배치 계산 toorun hello 사용자 지정 활동을 사용 합니다. 사용자 고유의 Windows 기반 HDInsight 클러스터를 사용 하거나 데이터 팩터리에 주문형 Windows 기반 HDInsight 클러스터를 만들고 hello HDInsight 클러스터에서 실행 하는 hello 사용자 지정 활동을 포함 한 수도 있습니다. HDInsight 클러스터를 사용 하기 위한 hello 상위 수준 단계는 다음과 같습니다.

> [!IMPORTANT]
> 사용자 지정.NET 작업 hello Windows 기반 HDInsight 클러스터에 대해서만 실행 합니다. 이 제한에 대 한 해결 방법은 toouse hello Linux 기반 HDInsight 클러스터에서 맵 줄일 활동 toorun 사용자 지정 Java 코드입니다. 두 번째 방법은 toouse Vm toorun HDInsight 클러스터를 사용 하는 대신 사용자 지정 활동의 Azure 배치 풀 합니다.
 

1. Azure HDInsight 연결된 서비스 만들기   
2. 사용 하 여 HDInsight는 연결 된 서비스 대신 **AzureBatchLinkedService** hello에 JSON을 파이프라인 합니다.

Tootest 하려는 경우 사용 하 여 hello 연습에서는 변경 **시작** 및 **끝** hello Azure HDInsight 서비스로 hello 시나리오를 테스트할 수 있도록 hello 파이프라인에 대 한 시간입니다.

#### <a name="create-azure-hdinsight-linked-service"></a>Azure HDInsight 연결된 서비스 만들기
주문형 클러스터 만들기를 지원 하 고 tooprocess 입력된 tooproduce 출력 데이터를 사용 하는 hello Azure 데이터 팩터리 서비스 합니다. 자체 클러스터를 사용할 수도 있습니다 tooperform hello 동일 합니다. 주문형 HDInsight 클러스터를 사용하면 각 조각에 대해 클러스터가 생성됩니다. 반면 hello 클러스터 준비는 사용자 고유의 HDInsight 클러스터를 사용할 경우 tooprocess 즉시 슬라이스를 hello 합니다. 따라서 주문형 클러스터를 사용할 때는 나타나지 않을 수 있습니다 hello 출력 데이터를 즉시 자체 클러스터를 사용 하는 경우.

> [!NOTE]
> 런타임 시.NET 활동의 인스턴스 hello HDInsight 클러스터의 작업자 노드 한 개 에서만 실행 여러 노드에 대해 크기 조정 된 toorun 수 없습니다. .NET 활동의 여러 인스턴스는 hello HDInsight 클러스터의 다른 노드에서 동시에 실행할 수 있습니다.
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse 주문형 HDInsight 클러스터
1. Hello에 **Azure 포털**, 클릭 **작성자 및 배포** hello Data Factory 홈 페이지에 있습니다.
2. 데이터 팩터리 편집기 hello 클릭 **새 계산** hello 명령 모음 및 선택에서 **주문형 HDInsight 클러스터** hello 메뉴에서 합니다.
3. Hello 다음 변경 내용을 toohello JSON 스크립트를 확인 합니다.

   1. Hello에 대 한 **clustersize는** 속성을 hello HDInsight 클러스터의 hello 크기를 지정 합니다.
   2. Hello에 대 한 **timeToLive** 속성을 기간 hello 고객 유휴 상태일 수 있는 삭제 하기 전에 지정 합니다.
   3. Hello에 대 한 **버전** 속성을 원하는 toouse hello HDInsight 버전을 지정 합니다. 이 속성을 제외 하면 hello 최신 버전이 사용 됩니다.  
   4. Hello에 대 한 **linkedServiceName**, 지정 **AzureStorageLinkedService**합니다.

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > 사용자 지정.NET 작업 hello Windows 기반 HDInsight 클러스터에 대해서만 실행 합니다. 이 제한에 대 한 해결 방법은 toouse hello Linux 기반 HDInsight 클러스터에서 맵 줄일 활동 toorun 사용자 지정 Java 코드입니다. 두 번째 방법은 toouse Vm toorun HDInsight 클러스터를 사용 하는 대신 사용자 지정 활동의 Azure 배치 풀 합니다.

4. 클릭 **배포** hello 명령 toodeploy hello 연결 된 서비스 모음에 있습니다.

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse 고유한 HDInsight 클러스터:
1. Hello에 **Azure 포털**, 클릭 **작성자 및 배포** hello Data Factory 홈 페이지에 있습니다.
2. Hello에 **데이터 팩터리 편집기**, 클릭 **새 계산** hello 명령 모음 및 선택에서 **HDInsight 클러스터** hello 메뉴에서 합니다.
3. Hello 다음 변경 내용을 toohello JSON 스크립트를 확인 합니다.

   1. Hello에 대 한 **clusterUri** 속성 HDInsight에 대 한 hello URL을 입력 합니다. 예를 들어 https://<clustername>.azurehdinsight.net/을 입력합니다.     
   2. Hello에 대 한 **UserName** 속성을 액세스 toohello HDInsight 클러스터를 가진 hello 사용자 이름을 입력 합니다.
   3. Hello에 대 한 **암호** 속성 hello 사용자 hello 암호를 입력 합니다.
   4. Hello에 대 한 **LinkedServiceName** 속성, 입력 **AzureStorageLinkedService**합니다.
4. 클릭 **배포** hello 명령 toodeploy hello 연결 된 서비스 모음에 있습니다.

자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md) 을 참조하세요.

Hello에 **JSON 파이프라인**, HDInsight를 사용 하 여 (요청 시 또는 직접) 연결 된 서비스:

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>.NET SDK를 사용하여 사용자 지정 작업 만들기
이 문서의 hello 연습에서는 hello Azure 포털을 사용 하 여 hello 사용자 지정 활동을 사용 하는 파이프라인을 사용 하 여 데이터 팩터리를 만듭니다. 코드 다음 hello toocreate 데이터 팩터리.NET SDK를 대신 사용 하 여 hello 하는 방법을 보여 줍니다. SDK tooprogrammatically 사용에 대 한 자세한 내용은 hello에서 파이프라인을 만들 것을 확인할 수 있습니다 [.NET API를 사용 하 여 복사 작업으로 파이프라인을 만들고](data-factory-copy-activity-tutorial-using-dotnet-api.md) 문서. 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>Visual Studio에서 사용자 지정 작업 디버깅
hello [Azure 데이터 팩터리-로컬 환경](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) GitHub에 샘플 Visual Studio 내에서 사용자 지정.NET 작업 toodebug 수 있는 도구를 포함 합니다.  


## <a name="sample-custom-activities-on-github"></a>GitHub의 샘플 사용자 지정 작업
| 샘플 | 사용자 지정 작업의 기능 |
| --- | --- |
| [HTTP 데이터 다운로더](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |HTTP 끝점 tooAzure Data Factory에 사용자 지정 C# 활동을 사용 하 여 Blob 저장소에서에서 데이터를 다운로드 합니다. |
| [Twitter 감성 분석 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |Azure ML 모델을 호출하고 감성 분석, 점수 매기기, 예측 등을 수행합니다. |
| [R 스크립트 실행](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |R이 이미 설치된 HDInsight 클러스터에서 RScript.exe를 실행하여 R 스크립트를 호출합니다. |
| [크로스 AppDomain .NET 작업](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |Hello 데이터 팩터리 시작 관리자에서 사용 하는 것에서 다른 어셈블리 버전을 사용 하 여 |
| [Azure Analysis Services에서 모델 다시 처리](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  Azure Analysis Services에서 모델을 다시 처리합니다. |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
