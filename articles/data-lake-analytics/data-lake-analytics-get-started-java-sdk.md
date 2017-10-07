---
title: "데이터 레이크 분석 Java SDK toodevelop 응용 프로그램 aaaUse | Microsoft Docs"
description: "Azure 데이터 레이크 분석 Java SDK toodevelop 응용 프로그램을 사용 하 여"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 07830b36-2fe3-4809-a846-129cf67b6a9e
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0d975812fe659ed34ee9befd37ee7c0bf50d3414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-java-sdk"></a><span data-ttu-id="7fe2d-103">Java SDK를 사용하여 Azure Data Lake Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="7fe2d-103">Get started with Azure Data Lake Analytics using Java SDK</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="7fe2d-104">어떻게 toouse hello Azure 데이터 레이크 분석 Java SDK toocreate Azure 데이터 레이크 계정 알아보고 등 폴더를 만들고 업로드 하 고 데이터 파일을 다운로드 하는 대로 사용자 계정을 삭제 한 항목과 작업을 처리 하는 기본 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-104">Learn how toouse hello Azure Data Lake Analytics Java SDK toocreate an Azure Data Lake account and perform basic operations such as create folders, upload and download data files, delete your account, and work with jobs.</span></span> <span data-ttu-id="7fe2d-105">Data Lake에 대한 자세한 내용은 [Azure Data Lake 분석](data-lake-analytics-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-105">For more information about Data Lake, see [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="7fe2d-106">이 자습서에서는 일반 관리 작업은 물론 테스트 데이터 생성 및 작업 제출 샘플을 포함하는 Java 콘솔 응용 프로그램을 개발합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-106">In this tutorial, you will develop a Java console application which contains samples of common administrative tasks as well as creating test data and submitting a job.</span></span>  <span data-ttu-id="7fe2d-107">다른를 사용 하 여 동일한 자습서 지원 hello 통해 toogo 도구는이 섹션의 hello 상단에서 hello 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-107">toogo through hello same tutorial using other supported tools, click hello tabs on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fe2d-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7fe2d-108">Prerequisites</span></span>
* <span data-ttu-id="7fe2d-109">JDK(Java Development Kit) 8 (Java 버전 1.8 사용).</span><span class="sxs-lookup"><span data-stu-id="7fe2d-109">Java Development Kit (JDK) 8 (using Java version 1.8).</span></span>
* <span data-ttu-id="7fe2d-110">IntelliJ 또는 다른 적절한 Java 개발 환경.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-110">IntelliJ or another suitable Java development environment.</span></span> <span data-ttu-id="7fe2d-111">선택 사항이지만 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-111">This is optional but recommended.</span></span> <span data-ttu-id="7fe2d-112">아래의 hello 지침 IntelliJ를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-112">hello instructions below use IntelliJ.</span></span>
* <span data-ttu-id="7fe2d-113">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-113">**An Azure subscription**.</span></span> <span data-ttu-id="7fe2d-114">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7fe2d-115">AAD(Azure Active Directory) 응용 프로그램을 만들고 **클라이언트 ID**, **테넌트 ID** 및 **키**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-115">Create an Azure Active Directory (AAD) application and retrieve its **Client ID**, **Tenant ID**, and **Key**.</span></span> <span data-ttu-id="7fe2d-116">AAD 응용 프로그램 및 지침에 대 한 자세한 내용은 방법에 대 한 tooget 클라이언트 ID 참조 [만드는 Active Directory 응용 프로그램 및 서비스 사용자 포털을 사용 하 여](../azure-resource-manager/resource-group-create-service-principal-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-116">For more information about AAD applications and instructions on how tooget a client ID, see [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="7fe2d-117">hello 회신 URI 및 키도 됩니다 hello 포털에서 사용할 수 있으면 만든 hello 응용 프로그램 및 생성 된 키.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-117">hello Reply URI and Key will also be available from hello portal once you have hello application created and key generated.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="7fe2d-118">Azure Active Directory를 사용하여 인증하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="7fe2d-118">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="7fe2d-119">에 대 한 코드를 제공 하는 hello 아래 코드 조각 **비 대화형** hello 응용 프로그램 자체 자격 증명을 제공 하는 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-119">hello code snippet below provides code for **non-interactive** authentication, where hello application provides its own credentials.</span></span>

<span data-ttu-id="7fe2d-120">이 자습서 toowork에 대 한 Azure에서 응용 프로그램 권한 toocreate 리소스 toogive를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-120">You will need toogive your application permission toocreate resources in Azure for this tutorial toowork.</span></span> <span data-ttu-id="7fe2d-121">**매우 권장** 이 자습서의 hello 목적을 위해 Azure 구독에서이 응용 프로그램 참가자 사용 권한을 tooa 새롭고 사용 되지 않는 빈 리소스 그룹만 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-121">It is **highly recommended** that you only give this application Contributor permissions tooa new, unused, and empty resource group in your Azure subscription for hello purposes of this tutorial.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="7fe2d-122">Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="7fe2d-122">Create a Java application</span></span>
1. <span data-ttu-id="7fe2d-123">IntelliJ 열고 hello를 사용 하 여 새 Java 프로젝트를 만들 **명령줄 앱** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-123">Open IntelliJ and create a new Java project using hello **Command Line App** template.</span></span>
2. <span data-ttu-id="7fe2d-124">Hello 화면 왼쪽에 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **프레임 워크 지원 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-124">Right-click on hello project on hello left-hand side of your screen and click **Add Framework Support**.</span></span> <span data-ttu-id="7fe2d-125">**Maven**을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-125">Choose **Maven** and click **OK**.</span></span>
3. <span data-ttu-id="7fe2d-126">새로 만든 열기 hello **"pom.xml"** 파일을 hello 텍스트 조각을 hello 사이 다음 추가  **\</version >** 태그 및 hello  **\< /프로젝트 >** 태그:</span><span class="sxs-lookup"><span data-stu-id="7fe2d-126">Open hello newly created **"pom.xml"** file and add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>

    >[!NOTE]
    ><span data-ttu-id="7fe2d-127">이 단계는 Azure 데이터 레이크 분석 SDK hello Maven에 있을 때까지 일시적입니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-127">This step is temporary until hello Azure Data Lake Analytics SDK is available in Maven.</span></span> <span data-ttu-id="7fe2d-128">이 문서는 hello SDK를 Maven에서 사용할 수 있는 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-128">This article will be updated once hello SDK is available in Maven.</span></span> <span data-ttu-id="7fe2d-129">모든 향후 업데이트 toothis SDK Maven 통해 사용할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-129">All future updates toothis SDK will be availble through Maven.</span></span>
    >

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
4. <span data-ttu-id="7fe2d-130">너무 이동**파일**, 다음 **설정**, 다음 **빌드**, **실행**, **배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-130">Go too**File**, then **Settings**, then **Build**, **Execution**, **Deployment**.</span></span> <span data-ttu-id="7fe2d-131">**빌드 도구**, **Maven**, **가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-131">Select **Build Tools**, **Maven**, **Importing**.</span></span> <span data-ttu-id="7fe2d-132">**Maven 프로젝트 자동으로 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-132">Then check **Import Maven projects automatically**.</span></span>
5. <span data-ttu-id="7fe2d-133">열기 **Main.java** hello로 바꾸기 hello 기존 코드 블록 코드를 다음 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-133">Open **Main.java** and replace hello existing code block with hello following code.</span></span> <span data-ttu-id="7fe2d-134">또한 같은 hello 코드 조각에서 호출 하는 매개 변수에 대 한 hello 값을 제공 **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_ resourceGroupName** 에 대 한 자리 표시자를 대체 하 고 **CLIENT-ID**, **클라이언트 암호**, **테 넌 트 ID**, 및  **구독 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-134">Also, provide hello values for parameters called out in hello code snippet, such as **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName** and replace placeholders for **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID**, and **SUBSCRIPTION-ID**.</span></span>

    <span data-ttu-id="7fe2d-135">이 코드 hello 데이터 레이크 저장소 및 Data Lake 분석 계정, hello 저장소에서 파일을 만들지를 만드는 과정을 통해 작업 실행, 작업 상태를 가져오기, 작업 출력을 다운로드 들어가고 hello 계정을 마지막으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-135">This code goes through hello process of creating Data Lake Store and Data Lake Analytics accounts, creating files in hello store, running a job, getting job status, downloading job output, and finally deleting hello account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7fe2d-136">Hello Azure 데이터 레이크 서비스의 알려진된 문제로 현재입니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-136">There is currently a known issue with hello Azure Data Lake Service.</span></span>  <span data-ttu-id="7fe2d-137">Hello 샘플 응용 프로그램 중단 될 때 오류가 발생, toomanually hello 데이터 레이크 저장소 및 Data Lake 분석 계정 삭제 hello 스크립트 만드는 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-137">If hello sample app is interrupted or encounters an error, you may need toomanually delete hello Data Lake Store & Data Lake Analytics accounts that hello script creates.</span></span>  <span data-ttu-id="7fe2d-138">Hello 포털 모르는 경우 hello [관리 Azure 데이터 레이크 분석 Azure 포털을 사용 하 여](data-lake-analytics-manage-use-portal.md) 시작 가이드 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-138">If you're not familiar with hello Portal, hello [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span></span>
   >
   >

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

                _clientSecret = "<CLIENT-SECRET>"; // TODO: For production scenarios, we recommend that you replace this line with a more secure way of acquiring hello application client secret, rather than hard-coding it in hello source code.

                String localFolderPath = "C:\\local_path\\"; // TODO: Change this tooany unused, new, empty folder on your local machine.

                // Authenticate
                ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
                SetupClients(creds);

                // Create Data Lake Store and Analytics accounts
                WaitForNewline("Authenticated.", "Creating NEW accounts.");
                CreateAccounts();
                WaitForNewline("Accounts created.", "Displaying accounts.");

                // List Data Lake Store and Analytics accounts that this app can access
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

                // Create a file in Data Lake Store: input1.csv
                // TODO: these change order in hello next patch
                byte[] bytesContents = "123,abc".getBytes();
                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, "/input1.csv", bytesContents, true);

                WaitForNewline("File created.", "Submitting a job.");

                // Submit a job tooData Lake Analytics
                UUID jobId = SubmitJobByScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input too@\"/output1.csv\" USING Outputters.Csv();", "testJob");
                WaitForNewline("Job submitted.", "Getting job status.");

                // Wait for job completion and output job status
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                System.out.println("Waiting for job completion.");
                WaitForJob(jobId);
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                WaitForNewline("Job completed.", "Downloading job output.");

                // Download job output from Data Lake Store
                DownloadFile("/output1.csv", localFolderPath + "output1.csv");
                WaitForNewline("Job output downloaded.", "Deleting file.");

                // Delete file from Data Lake Store
                DeleteFile("/output1.csv");
                WaitForNewline("File deleted.", "Deleting account.");

                // Delete account
                _adlsClient.getAccountOperations().delete(_resourceGroupName, _adlsAccountName);
                _adlaClient.getAccountOperations().delete(_resourceGroupName, _adlaAccountName);
                WaitForNewline("Account deleted.", "DONE.");
            }

            //Set up clients
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

            // Helper function tooshow status and wait for user input
            public static void WaitForNewline(String reason, String nextAction)
            {
                if (nextAction == null)
                    nextAction = "";

                System.out.println(reason + "\r\nPress ENTER toocontinue...");
                try{System.in.read();}
                catch(Exception e){}

                if (!nextAction.isEmpty())
                {
                    System.out.println(nextAction);
                }
            }

            // Create Data Lake Store and Analytics accounts
            public static void CreateAccounts() throws InterruptedException, CloudException, IOException {
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

                    /* If this line generates an error message like "hello deep update for property 'DataLakeStoreAccounts' is not supported", please delete hello ADLS and ADLA accounts via hello portal and re-run your script. */

                _adlaClient.getAccountOperations().create(_resourceGroupName, _adlaAccountName, adlaParameters);
            }

            //todo: this changes in hello next version of hello API
            public static void CreateFile(String path, String contents, boolean force) throws IOException, CloudException {
                byte[] bytesContents = contents.getBytes();

                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, path, bytesContents, force);
            }

            public static void DeleteFile(String filePath) throws IOException, CloudException {
                _adlsFileSystemClient.getFileSystemOperations().delete(filePath, _adlsAccountName);
            }

            // Download file
            public static void DownloadFile(String srcPath, String destPath) throws IOException, CloudException {
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

            // Submit a U-SQL job by providing script contents.
            // Returns hello job ID
            public static UUID SubmitJobByScript(String script, String jobName) throws IOException, CloudException {
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
            public static JobResult WaitForJob(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                while (jobInfo.getState() != JobState.ENDED)
                {
                    jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName,jobId).getBody();
                }
                return jobInfo.getResult();
            }

            // Get job status
            public static String GetJobStatus(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                return jobInfo.getState().toValue();
            }
        }

1. <span data-ttu-id="7fe2d-139">Hello 프롬프트 toorun 및 전체 hello 응용 프로그램을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-139">Follow hello prompts toorun and complete hello application.</span></span>

## <a name="see-also"></a><span data-ttu-id="7fe2d-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7fe2d-140">See also</span></span>
* <span data-ttu-id="7fe2d-141">toosee hello 같은 다른 도구를 사용 하 여 자습서 hello hello 페이지 위쪽에 hello 탭 선택기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-141">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="7fe2d-142">toosee 복잡 한 쿼리를 참조 [분석 웹 사이트 Azure 데이터 레이크 분석을 사용 하 여 로그](data-lake-analytics-analyze-weblogs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-142">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="7fe2d-143">U-SQL 응용 프로그램 개발 시작 tooget 참조 [데이터 레이크 도구를 사용 하 여 Visual Studio에 대 한 개발 U-SQL 스크립트](data-lake-analytics-data-lake-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-143">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="7fe2d-144">toolearn U SQL 참조 [Azure 데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md), 및 [U SQL 언어 참조](http://go.microsoft.com/fwlink/?LinkId=691348)합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-144">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="7fe2d-145">관리 작업을 보려면 [Azure 포털을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-145">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="7fe2d-146">데이터 레이크 분석의 개요는 tooget 참조 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7fe2d-146">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
