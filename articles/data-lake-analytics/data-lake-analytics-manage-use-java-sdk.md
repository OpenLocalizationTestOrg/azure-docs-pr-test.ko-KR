---
title: "Azure Java SDK를 사용하여 Azure Data Lake Analytics 관리 | Microsoft Docs"
description: "Azure Data Lake 분석 Java SDK를 사용하여 응용 프로그램 개발"
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: 07830b36-2fe3-4809-a846-129cf67b6a9e
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 8a0c1c7aab89f3bb62d0eb9f42e8ac65309d617e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage--azure-data-lake-analytics-using-java-sdk"></a><span data-ttu-id="b7707-103">Java SDK를 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="b7707-103">Manage  Azure Data Lake Analytics using Java SDK</span></span>

<span data-ttu-id="b7707-104">이 자습서에서는 Azure Data Lake에 대한 일반적인 작업을 수행하는 Java 콘솔 응용 프로그램을 개발합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-104">In this tutorial, you develop a Java console application that performs common operations for Azure Data Lake.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7707-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b7707-105">Prerequisites</span></span>
* <span data-ttu-id="b7707-106">**JDK(Java Development Kit) 8**(Java 버전 1.8 사용)</span><span class="sxs-lookup"><span data-stu-id="b7707-106">**Java Development Kit (JDK) 8** (using Java version 1.8).</span></span>
* <span data-ttu-id="b7707-107">**IntelliJ** 또는 다른 적절한 Java 개발 환경.</span><span class="sxs-lookup"><span data-stu-id="b7707-107">**IntelliJ** or another suitable Java development environment.</span></span> <span data-ttu-id="b7707-108">이 문서의 지침에서는 IntelliJ를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-108">The instructions in this document use IntelliJ.</span></span>
* <span data-ttu-id="b7707-109">AAD(Azure Active Directory) 응용 프로그램을 만들고 **클라이언트 ID**, **테넌트 ID** 및 **키**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-109">Create an Azure Active Directory (AAD) application and retrieve its **Client ID**, **Tenant ID**, and **Key**.</span></span> <span data-ttu-id="b7707-110">AAD 응용 프로그램에 대한 자세한 내용 및 클라이언트 ID를 가져오는 방법에 대한 지침은 [포털을 사용하여 Active Directory 응용 프로그램 및 서비스 주체 만들기](../azure-resource-manager/resource-group-create-service-principal-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7707-110">For more information about AAD applications and instructions on how to get a client ID, see [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="b7707-111">응용 프로그램을 만들고 키를 생성했다면 회신 URI 및 키를 포털에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-111">The Reply URI and Key is available from the portal once you have the application created and key generated.</span></span>

## <a name="authenticating-using-azure-active-directory"></a><span data-ttu-id="b7707-112">Azure Active Directory를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="b7707-112">Authenticating using Azure Active Directory</span></span>

<span data-ttu-id="b7707-113">다음 코드 조각은 응용 프로그램이 자체 자격 증명을 제공하는 **비대화형** 인증에 대한 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-113">The code following snippet provides code for **non-interactive** authentication, where the application provides its own credentials.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="b7707-114">Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b7707-114">Create a Java application</span></span>
1. <span data-ttu-id="b7707-115">**명령줄 앱** 템플릿을 사용하여 IntelliJ를 열고 Java 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-115">Open IntelliJ and create a Java project using the **Command-Line App** template.</span></span>
2. <span data-ttu-id="b7707-116">화면의 왼쪽에 있는 프로젝트를 마우스 오른쪽 단추로 클릭하고 **프레임워크 지원 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-116">Right-click on the project on the left-hand side of your screen and click **Add Framework Support**.</span></span> <span data-ttu-id="b7707-117">**Maven**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-117">Choose **Maven** and click **OK**.</span></span>
3. <span data-ttu-id="b7707-118">새로 만든 **"pom.xml"** 파일을 열고 **\</version>** 태그 및 **\</project>** 태그 사이에 다음 텍스트의 코드 조각을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-118">Open the newly created **"pom.xml"** file and add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>

```
<repositories>
    <repository>
        <id>adx-snapshots</id>
        <name>Azure ADX Snapshots</name>
        <url>http://adxsnapshots.azurewebsites.net/</url>
        <layout>default</layout>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </repository>
    <repository>
        <id>oss-snapshots</id>
        <name>Open Source Snapshots</name>
        <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
        <layout>default</layout>
        <snapshots>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
        </snapshots>
    </repository>
</repositories>
<dependencies>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-client-authentication</artifactId>
        <version>1.0.0-20160513.000802-24</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-client-runtime</artifactId>
        <version>1.0.0-20160513.000812-28</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.rest</groupId>
        <artifactId>client-runtime</artifactId>
        <version>1.0.0-20160513.000825-29</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-mgmt-datalake-store</artifactId>
        <version>1.0.0-SNAPSHOT</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-mgmt-datalake-analytics</artifactId>
        <version>1.0.0-SNAPSHOT</version>
    </dependency>
</dependencies>
```

<span data-ttu-id="b7707-119">**파일 > 설정 > 빌드 > 실행 > 배포**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-119">Go to **File > Settings > Build > Execution > Deployment**.</span></span> <span data-ttu-id="b7707-120">**빌드 도구 > Maven > 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-120">Select **Build Tools > Maven > Importing**.</span></span> <span data-ttu-id="b7707-121">**Maven 프로젝트 자동으로 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-121">Then check **Import Maven projects automatically**.</span></span>

<span data-ttu-id="b7707-122">`Main.java`를 열고 기존 코드 블록을 다음 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-122">Open `Main.java` and replace the existing code block with the following code snippet:</span></span>

```
package com.company;

import com.microsoft.azure.CloudException;
import com.microsoft.azure.credentials.ApplicationTokenCredentials;
import com.microsoft.azure.management.datalake.store.*;
import com.microsoft.azure.management.datalake.store.models.*;
import com.microsoft.azure.management.datalake.analytics.*;
import com.microsoft.azure.management.datalake.analytics.models.*;
import com.microsoft.rest.credentials.ServiceClientCredentials;
import java.io.*;
import java.nio.charset.Charset;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.UUID;
import java.util.List;

public class Main {
    private static String _adlsAccountName;
    private static String _adlaAccountName;
    private static String _resourceGroupName;
    private static String _location;

    private static String _tenantId;
    private static String _subId;
    private static String _clientId;
    private static String _clientSecret;

    private static DataLakeStoreAccountManagementClient _adlsClient;
    private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;
    private static DataLakeAnalyticsAccountManagementClient _adlaClient;
    private static DataLakeAnalyticsJobManagementClient _adlaJobClient;
    private static DataLakeAnalyticsCatalogManagementClient _adlaCatalogClient;

    public static void main(String[] args) throws Exception {

        _adlsAccountName = "<DATA-LAKE-STORE-NAME>";
        _adlaAccountName = "<DATA-LAKE-ANALYTICS-NAME>";
        _resourceGroupName = "<RESOURCE-GROUP-NAME>";
        _location = "East US 2";

        _tenantId = "<TENANT-ID>";
        _subId =  "<SUBSCRIPTION-ID>";
        _clientId = "<CLIENT-ID>";

        _clientSecret = "<CLIENT-SECRET>"; 
        
        String localFolderPath = "C:\\local_path\\"; 
        
        // ----------------------------------------
        // Authenticate
        // ----------------------------------------
        ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
        SetupClients(creds);

        // ----------------------------------------
        // List Data Lake Store and Analytics accounts that this app can access
        // ----------------------------------------
        System.out.println(String.format("All ADL Store accounts that this app can access in subscription %s:", _subId));
        List<DataLakeStoreAccount> adlsListResult = _adlsClient.getAccountOperations().list().getBody();
        for (DataLakeStoreAccount acct : adlsListResult) {
            System.out.println(acct.getName());
        }
        
        System.out.println(String.format("All ADL Analytics accounts that this app can access in subscription %s:", _subId));
        List<DataLakeAnalyticsAccount> adlaListResult = _adlaClient.getAccountOperations().list().getBody();
        for (DataLakeAnalyticsAccount acct : adlaListResult) {
            System.out.println(acct.getName());
        }
        WaitForNewline("Accounts displayed.", "Creating files.");

        // ----------------------------------------
        // Create a file in Data Lake Store: input1.csv
        // ----------------------------------------

        byte[] bytesContents = "123,abc".getBytes();
        _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, "/input1.csv", bytesContents, true);

        WaitForNewline("File created.", "Submitting a job.");

        // ----------------------------------------
        // Submit a job to Data Lake Analytics
        // ----------------------------------------

string script = "@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();", "testJob";
        UUID jobId = SubmitJobByScript(script);
        WaitForNewline("Job submitted.", "Getting job status.");

        // ----------------------------------------
        // Wait for job completion and output job status
        // ----------------------------------------
        System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
        System.out.println("Waiting for job completion.");
        WaitForJob(jobId);
        System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
        WaitForNewline("Job completed.", "Downloading job output.");

        // ----------------------------------------
        // Download job output from Data Lake Store
        // ----------------------------------------
        DownloadFile("/output1.csv", localFolderPath + "output1.csv");
        WaitForNewline("Job output downloaded.", "Deleting file.");

    }
}
```

<span data-ttu-id="b7707-123">코드 조각에서 호출되는 매개 변수 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-123">Provide the values for parameters called out in the code snippet:</span></span>
* `localFolderPath`
* `_adlaAccountName`
* `_adlsAccountName`
* `_resourceGroupName`

<span data-ttu-id="b7707-124">다음의 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7707-124">Replace the placeholders for:</span></span>
* <span data-ttu-id="b7707-125">`CLIENT-ID`,</span><span class="sxs-lookup"><span data-stu-id="b7707-125">`CLIENT-ID`,</span></span>
* <span data-ttu-id="b7707-126">`CLIENT-SECRET`,</span><span class="sxs-lookup"><span data-stu-id="b7707-126">`CLIENT-SECRET`,</span></span>
* `TENANT-ID`
* `SUBSCRIPTION-ID`

## <a name="helper-functions"></a><span data-ttu-id="b7707-127">도우미 함수</span><span class="sxs-lookup"><span data-stu-id="b7707-127">Helper functions</span></span>

### <a name="setup-clients"></a><span data-ttu-id="b7707-128">클라이언트 설치</span><span class="sxs-lookup"><span data-stu-id="b7707-128">Setup clients</span></span>

```
public static void SetupClients(ServiceClientCredentials creds)
{
    _adlsClient = new DataLakeStoreAccountManagementClientImpl(creds);
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClientImpl(creds);
    _adlaClient = new DataLakeAnalyticsAccountManagementClientImpl(creds);
    _adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);
    _adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClientImpl(creds);
    _adlsClient.setSubscriptionId(_subId);
    _adlaClient.setSubscriptionId(_subId);
}
```


### <a name="wait-for-input"></a><span data-ttu-id="b7707-129">입력 대기</span><span class="sxs-lookup"><span data-stu-id="b7707-129">Wait for input</span></span>

```
public static void WaitForNewline(String reason, String nextAction)
{
    if (nextAction == null)
        nextAction = "";

    System.out.println(reason + "\r\nPress ENTER to continue...");
    try{System.in.read();}
    catch(Exception e){}

    if (!nextAction.isEmpty())
    {
        System.out.println(nextAction);
    }
}
```

### <a name="create-accounts"></a><span data-ttu-id="b7707-130">계정 만들기</span><span class="sxs-lookup"><span data-stu-id="b7707-130">Create accounts</span></span>

```
public static void CreateAccounts() throws InterruptedException, CloudException, IOException 
{
    // Create ADLS account
    DataLakeStoreAccount adlsParameters = new DataLakeStoreAccount();
    adlsParameters.setLocation(_location);

    _adlsClient.getAccountOperations().create(_resourceGroupName, _adlsAccountName, adlsParameters);

    // Create ADLA account
    DataLakeStoreAccountInfo adlsInfo = new DataLakeStoreAccountInfo();
    adlsInfo.setName(_adlsAccountName);

    DataLakeStoreAccountInfoProperties adlsInfoProperties = new DataLakeStoreAccountInfoProperties();
    adlsInfo.setProperties(adlsInfoProperties);

    List<DataLakeStoreAccountInfo> adlsInfoList = new ArrayList<DataLakeStoreAccountInfo>();
    adlsInfoList.add(adlsInfo);

    DataLakeAnalyticsAccountProperties adlaProperties = new DataLakeAnalyticsAccountProperties();
    adlaProperties.setDataLakeStoreAccounts(adlsInfoList);
    adlaProperties.setDefaultDataLakeStoreAccount(_adlsAccountName);

    DataLakeAnalyticsAccount adlaParameters = new DataLakeAnalyticsAccount();
    adlaParameters.setLocation(_location);
    adlaParameters.setName(_adlaAccountName);
    adlaParameters.setProperties(adlaProperties);

    _adlaClient.getAccountOperations().create(_resourceGroupName, _adlaAccountName, adlaParameters);
}
```

### <a name="create-a-file"></a><span data-ttu-id="b7707-131">파일 만들기</span><span class="sxs-lookup"><span data-stu-id="b7707-131">Create a file</span></span>

```
public static void CreateFile(String path, String contents, boolean force) throws IOException, CloudException 
{
    byte[] bytesContents = contents.getBytes();

    _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, path, bytesContents, force);
}
```

### <a name="delete-a-file"></a><span data-ttu-id="b7707-132">파일 삭제</span><span class="sxs-lookup"><span data-stu-id="b7707-132">Delete a file</span></span>

```
public static void DeleteFile(String filePath) throws IOException, CloudException 
{
    _adlsFileSystemClient.getFileSystemOperations().delete(filePath, _adlsAccountName);
}
```

### <a name="download-a-file"></a><span data-ttu-id="b7707-133">파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="b7707-133">Download a file</span></span>

```
public static void DownloadFile(String srcPath, String destPath) throws IOException, CloudException 
{
    InputStream stream = _adlsFileSystemClient.getFileSystemOperations().open(srcPath, _adlsAccountName).getBody();

    PrintWriter pWriter = new PrintWriter(destPath, Charset.defaultCharset().name());

    String fileContents = "";
    if (stream != null) {
        Writer writer = new StringWriter();

        char[] buffer = new char[1024];
        try {
            Reader reader = new BufferedReader(
                    new InputStreamReader(stream, "UTF-8"));
            int n;
            while ((n = reader.read(buffer)) != -1) {
                writer.write(buffer, 0, n);
            }
        } finally {
            stream.close();
        }
        fileContents =  writer.toString();
    }

    pWriter.println(fileContents);
    pWriter.close();
}
```

### <a name="submit-a-u-sql-job"></a><span data-ttu-id="b7707-134">U-SQL 작업 제출</span><span class="sxs-lookup"><span data-stu-id="b7707-134">Submit a U-SQL job</span></span>

```
public static UUID SubmitJobByScript(String script, String jobName) throws IOException, CloudException 
{
    UUID jobId = java.util.UUID.randomUUID();
    USqlJobProperties properties = new USqlJobProperties();
    properties.setScript(script);
    JobInformation parameters = new JobInformation();
    parameters.setName(jobName);
    parameters.setJobId(jobId);
    parameters.setType(JobType.USQL);
    parameters.setProperties(properties);

    JobInformation jobInfo = _adlaJobClient.getJobOperations().create(_adlaAccountName, jobId, parameters).getBody();

    return jobId;
}

// Wait for job completion
public static JobResult WaitForJob(UUID jobId) throws IOException, CloudException 
{
    JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
    while (jobInfo.getState() != JobState.ENDED)
    {
        jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName,jobId).getBody();
    }
    return jobInfo.getResult();
}
```

### <a name="retrieve-job-status"></a><span data-ttu-id="b7707-135">작업 상태 검색</span><span class="sxs-lookup"><span data-stu-id="b7707-135">Retrieve job status</span></span>

```
public static String GetJobStatus(UUID jobId) throws IOException, CloudException 
{
    JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
    return jobInfo.getState().toValue();
}
```

## <a name="next-steps"></a><span data-ttu-id="b7707-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7707-136">Next steps</span></span>

* <span data-ttu-id="b7707-137">U-SQL에 대해 알아보려면 [Azure Data Lake Analytics U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md) 및 [U-SQL 언어 참조](http://go.microsoft.com/fwlink/?LinkId=691348)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7707-137">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="b7707-138">관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7707-138">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="b7707-139">데이터 레이크 분석에 대한 개요를 보려면 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7707-139">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
