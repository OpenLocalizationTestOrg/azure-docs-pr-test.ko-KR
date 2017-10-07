---
title: "Azure 명령줄 2.0 aaaUse 인터페이스 tooget Azure 데이터 레이크 저장소 시작 | Microsoft Docs"
description: "Azure 크로스 플랫폼 명령줄 2.0 toocreate 데이터 레이크 저장소 계정을 사용 하 고 기본 작업 수행"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="ce01d-103">Azure CLI 2.0을 사용하여 Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="ce01d-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce01d-104">포털</span><span class="sxs-lookup"><span data-stu-id="ce01d-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="ce01d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce01d-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="ce01d-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="ce01d-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="ce01d-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="ce01d-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="ce01d-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ce01d-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="ce01d-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ce01d-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="ce01d-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ce01d-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="ce01d-111">Python</span><span class="sxs-lookup"><span data-stu-id="ce01d-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="ce01d-112">Azure 데이터 레이크는 저장 하는 Azure CLI 2.0 toouse toocreate 방법에 대해 알아봅니다 계정 및 폴더를 만들어 업로드 및 다운로드 데이터 파일 등의 기본 작업 수행, 계정, 등을 삭제 합니다. Data Lake Store에 대한 자세한 내용은 [Data Lake Store 개요](data-lake-store-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce01d-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="ce01d-113">hello Azure CLI 2.0은 Azure 리소스 관리를 위해 Azure의 새로운 명령줄 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="ce01d-114">macOS, Linux 및 Windows에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="ce01d-115">자세한 내용은 [Azure CLI 2.0 개요](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce01d-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="ce01d-116">Hello을 살펴볼 수도 있습니다 [Azure 데이터 레이크 저장소 CLI 2.0 참조](https://docs.microsoft.com/cli/azure/dls) 명령 및 구문을의 전체 목록은 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ce01d-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ce01d-117">Prerequisites</span></span>
<span data-ttu-id="ce01d-118">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="ce01d-119">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="ce01d-119">**An Azure subscription**.</span></span> <span data-ttu-id="ce01d-120">[Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce01d-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="ce01d-121">**Azure CLI 2.0** - 지침은 [Install Azure CLI 2.0 설치](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce01d-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="ce01d-122">인증</span><span class="sxs-lookup"><span data-stu-id="ce01d-122">Authentication</span></span>

<span data-ttu-id="ce01d-123">이 문서는 최종 사용자로 로그인하는 Data Lake Store에 보다 간단한 인증 방식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="ce01d-124">hello 액세스 수준 tooData Lake 저장소 계정 및 파일 시스템은 다음 hello 로그인 한 사용자의 hello 액세스 수준을 통해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="ce01d-125">그러나 여러 가지 다른 접근 방법이 데이터 레이크 저장소와 잘 tooauthenticate로 요소인 **최종 사용자 인증** 또는 **서비스 간 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="ce01d-126">지침 및 방법에 대 한 자세한 내용은 tooauthenticate, 참조 [최종 사용자 인증](data-lake-store-end-user-authenticate-using-active-directory.md) 또는 [서비스 간 인증](data-lake-store-authenticate-using-active-directory.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="ce01d-127">Azure 구독 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="ce01d-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="ce01d-128">Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="ce01d-129">Hello 다음 단계에서 코드 toouse를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="ce01d-130">웹 브라우저 tooopen hello 페이지 https://aka.ms/devicelogin를 사용 하 고 hello 코드 tooauthenticate를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="ce01d-131">자격 증명을 사용 하 여 증명된 toolog 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="ce01d-132">모든 hello 창 목록에 로그인 hello 사용자 계정과 연결 된 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="ce01d-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="ce01d-133">다음 명령 toouse 특정 구독 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="ce01d-134">Azure 데이터 레이크 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ce01d-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="ce01d-135">새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-135">Create a new resource group.</span></span> <span data-ttu-id="ce01d-136">다음 명령을 hello, hello toouse 원하는 매개 변수 값 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="ce01d-137">Hello 위치 이름에 공백이 포함 되어 있으면 따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="ce01d-138">예를 들어 "East US 2"입니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="ce01d-139">Hello 데이터 레이크 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="ce01d-140">Data Lake 저장소 계정에서 폴더 만들기</span><span class="sxs-lookup"><span data-stu-id="ce01d-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="ce01d-141">Azure 데이터 레이크 저장소 계정 toomanage에서 폴더를 만들고 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="ce01d-142">사용 하 여 hello 명령 toocreate는 폴더의 이름은 다음 **mynewfolder** hello hello 데이터 레이크 저장소 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="ce01d-143">hello `--folder` 매개 변수를 사용 하면 hello 명령 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="ce01d-144">이 매개 변수가 없으면 hello 명령은 mynewfolder hello 루트 hello Data Lake 저장소 계정에 라는 빈 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="ce01d-145">데이터 tooa Data Lake 저장소 계정에 업로드</span><span class="sxs-lookup"><span data-stu-id="ce01d-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="ce01d-146">Hello 루트 수준 또는 tooa 만든 폴더에 hello 계정 내에서 직접 데이터 tooData Lake 저장소에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="ce01d-147">아래 hello 조각은 보여 방법을 tooupload 일부 예제 데이터 toohello 폴더 (**mynewfolder**) hello 이전 섹션에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="ce01d-148">몇 가지 샘플 데이터 tooupload를 찾고 hello를 얻을 수 있습니다 **Ambulance 데이터** hello 폴더 [Azure 데이터 레이크 Git 리포지토리](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="ce01d-149">Hello 파일을 다운로드 하 고 C:\sampledata\ 같은 컴퓨터에 로컬 디렉터리에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="ce01d-150">Hello 대상에 대 한 hello hello 파일 이름을 포함 하는 전체 경로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="ce01d-151">Data Lake Store 계정의 파일 나열</span><span class="sxs-lookup"><span data-stu-id="ce01d-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="ce01d-152">데이터 레이크 저장소 계정에서 명령 toolist hello 파일을 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="ce01d-153">이 hello 출력 비슷한 toohello 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-153">hello output of this should be similar toohello following:</span></span>

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="ce01d-154">Data Lake Store 계정에서 데이터 이름 바꾸기, 다운로드 및 삭제</span><span class="sxs-lookup"><span data-stu-id="ce01d-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="ce01d-155">**toorename 파일**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ce01d-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="ce01d-156">**toodownload 파일**, hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="ce01d-157">이미 지정 hello 대상 경로가 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="ce01d-158">존재 하지 않는 경우 hello 명령은 hello 대상 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="ce01d-159">**toodelete 파일**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ce01d-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="ce01d-160">Toodelete hello 폴더가 **mynewfolder** 및 hello 파일 **vehicle1_09142014_copy.csv** 함께 하나의 명령으로 사용 하 여 hello-매개 변수를 recurse</span><span class="sxs-lookup"><span data-stu-id="ce01d-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="ce01d-161">Data Lake Store 계정에 대한 ACL 및 사용 권한 작업</span><span class="sxs-lookup"><span data-stu-id="ce01d-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="ce01d-162">이 섹션에서는 방법에 대 한 설명 toomanage Acl 및 Azure CLI 2.0을 사용 하 여 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="ce01d-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="ce01d-163">Azure Data Lake Store에서 ACL을 구현하는 방법에 대한 자세한 내용은 [Data Lake Store에서 액세스 제어 개요](data-lake-store-access-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce01d-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="ce01d-164">**파일/폴더의 tooupdate hello 소유자**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ce01d-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="ce01d-165">**파일/폴더에 대 한 tooupdate hello 권한을**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ce01d-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="ce01d-166">**지정된 된 경로 대 한 Acl tooget hello**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ce01d-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="ce01d-167">hello 출력은 비슷한 toohello 다음 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-167">hello output should be similar toohello following:</span></span>

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* <span data-ttu-id="ce01d-168">**ACL에 대 한 항목이 tooset**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ce01d-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="ce01d-169">**ACL에 대 한 항목이 tooremove**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ce01d-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="ce01d-170">**전체 기본 ACL tooremove**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ce01d-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="ce01d-171">**전체 기본이 아닌 ACL tooremove**, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ce01d-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="ce01d-172">Data Lake 저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="ce01d-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="ce01d-173">다음 명령 toodelete 데이터 레이크 저장소 계정 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce01d-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="ce01d-174">메시지가 표시 되 면 입력 **Y** toodelete hello 계정.</span><span class="sxs-lookup"><span data-stu-id="ce01d-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce01d-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce01d-175">Next steps</span></span>

* [<span data-ttu-id="ce01d-176">Azure Data Lake Store CLI 2.0 참조</span><span class="sxs-lookup"><span data-stu-id="ce01d-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="ce01d-177">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="ce01d-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="ce01d-178">Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="ce01d-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ce01d-179">Azure HDInsight에 데이터 레이크 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="ce01d-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
