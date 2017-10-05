---
title: "Azure CLI를 사용하여 Azure 앱에 대한 ID 만들기 | Microsoft Docs"
description: "Azure CLI를 사용하여 Azure Active Directory 응용 프로그램 및 서비스 주체를 만들고 역할 기반 액세스 제어를 통해 리소스에 대한 액세스를 부여하는 방법을 설명합니다. 암호 또는 인증서를 사용하여 응용 프로그램을 인증하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 3c5826d58887ff1af4df8e66999d9c1a1643bcc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="6c121-104">Azure CLI를 사용하여 리소스에 액세스하는 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="6c121-104">Use Azure CLI to create a service principal to access resources</span></span>

<span data-ttu-id="6c121-105">리소스에 액세스해야 하는 앱 또는 스크립트가 있는 경우 앱에 대한 ID를 설정하고 자체 자격 증명으로 앱을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="6c121-106">이 ID를 서비스 주체라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-106">This identity is known as a service principal.</span></span> <span data-ttu-id="6c121-107">이 접근 방법을 사용하면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-107">This approach enables you to:</span></span>

* <span data-ttu-id="6c121-108">자체 사용 권한과 다른 앱 ID에 대한 사용 권한을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="6c121-109">일반적으로 이러한 권한은 정확히 앱 실행에 필요한 것으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="6c121-110">무인 스크립트를 실행할 때 인증을 위해 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="6c121-111">이 문서에서는 [Azure CLI 1.0](../cli-install-nodejs.md)을 사용하여 응용 프로그램을 자체 자격 증명 및 ID로 실행하도록 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-111">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="6c121-112">최신 버전의 [Azure CLI 1.0](../cli-install-nodejs.md)을 설치하여 환경이 이 문서의 예제와 일치하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-112">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="6c121-113">필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="6c121-113">Required permissions</span></span>
<span data-ttu-id="6c121-114">이 항목을 완료하려면 Azure Active Directory와 Azure 구독에 대한 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-114">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="6c121-115">특히, Azure Active Directory에서 앱을 만들고 역할에 서비스 주체를 할당할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-115">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="6c121-116">계정에 적절한 사용 권한이 있는지를 확인하는 가장 쉬운 방법은 포털을 통하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-116">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="6c121-117">[포털에서 필요한 사용 권한 확인](resource-group-create-service-principal-portal.md#required-permissions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="6c121-118">이제 [암호](#create-service-principal-with-password) 또는 [인증서](#create-service-principal-with-certificate) 인증에 대한 섹션을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-118">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="6c121-119">암호를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="6c121-119">Create service principal with password</span></span>
<span data-ttu-id="6c121-120">이 섹션에서는 암호를 사용하여 AD 응용 프로그램을 만드는 단계를 수행하고 읽기 권한자 역할을 서비스 주체에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-120">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="6c121-121">계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-121">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="6c121-122">앱 ID를 만들려면 다음 명령을 표시된 것처럼 앱의 이름과 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-122">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="6c121-123">새 서비스 주체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-123">The new service principal is returned.</span></span> <span data-ttu-id="6c121-124">사용 권한을 부여할 때 개체 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-124">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="6c121-125">로그인할 때 서비스 주체 이름으로 나열된 GUID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-125">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="6c121-126">이 GUID는 앱 ID와 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-126">This guid is the same value as the app id.</span></span> <span data-ttu-id="6c121-127">샘플 응용 프로그램에서 이 값은 `Client ID`라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-127">In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="6c121-128">서비스 사용자에게 구독에 대한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-128">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="6c121-129">이 예제에서는 구독에서 모든 리소스를 읽을 수 있는 권한이 부여된 읽기 권한자 역할에 서비스 주체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-129">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="6c121-130">다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-130">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="6c121-131">objectid 매개 변수의 경우 응용 프로그램을 만들 때 사용한 개체 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-131">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="6c121-132">이 명령을 실행하기 전에 새 서비스 주체가 Azure Active Directory 전체에 전파될 어느 정도의 시간을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-132">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="6c121-133">이러한 명령을 수동으로 실행할 때 작업 간에 충분 한 시간이 경과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-133">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="6c121-134">스크립트에 명령 사이에 절전 모드로 전환하는 단계를 추가해야 합니다(예시 `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="6c121-134">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="6c121-135">주체가 디렉터리에 존재하지 않는다는 오류가 표시되는 경우 명령을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-135">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="6c121-136">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-136">That's it!</span></span> <span data-ttu-id="6c121-137">AD 응용 프로그램 및 서비스 주체가 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-137">Your AD application and service principal are set up.</span></span> <span data-ttu-id="6c121-138">다음 섹션에서는 Azure CLI를 통해 자격 증명을 사용하여 로그인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-138">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="6c121-139">코드 응용 프로그램에서 자격 증명을 사용하려는 경우 이 항목을 진행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-139">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="6c121-140">[샘플 응용 프로그램](#sample-applications) 으로 이동하여 응용 프로그램 ID 및 암호를 사용하여 로그인하는 예제를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-140">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="6c121-141">Azure CLI를 통해 자격 증명 제공</span><span class="sxs-lookup"><span data-stu-id="6c121-141">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="6c121-142">이제 응용 프로그램으로 로그인하여 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-142">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="6c121-143">서비스 주체로 로그인할 때마다 AD 앱에 디렉터리의 테넌트 ID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-143">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="6c121-144">테넌트는 Azure Active Directory의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-144">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="6c121-145">현재 인증된 구독에 대한 테넌트 ID를 검색하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-145">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="6c121-146">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-146">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="6c121-147">다른 구독의 테넌트 ID를 가져와야 하는 경우 다음 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-147">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="6c121-148">로그인에 사용할 클라이언트 ID를 검색해야 하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-148">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="6c121-149">로그인에 사용할 값은 서비스 주체 이름에 나열된 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-149">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="6c121-150">서비스 주체로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-150">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="6c121-151">암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-151">You are prompted for the password.</span></span> <span data-ttu-id="6c121-152">AD 응용 프로그램을 만들 때 지정한 암호를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-152">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="6c121-153">이제 사용자는 작성한 서비스 주체에 대한 서비스 주체로 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-153">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="6c121-154">또는 명령줄에서 REST 작업을 호출하여 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-154">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="6c121-155">인증 응답에서 다른 작업에 사용할 액세스 토큰을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-155">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="6c121-156">REST 작업을 호출하여 액세스 토큰을 검색하는 예제는 [액세스 토큰 생성하기](resource-manager-rest-api.md#generating-an-access-token)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-156">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="6c121-157">인증서를 사용하여 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="6c121-157">Create service principal with certificate</span></span>
<span data-ttu-id="6c121-158">이 섹션에서 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-158">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="6c121-159">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="6c121-159">create a self-signed certificate</span></span>
* <span data-ttu-id="6c121-160">인증서를 사용하는 AD 응용 프로그램과 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="6c121-160">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="6c121-161">읽기 권한자 역할을 서비스 주체에 할당</span><span class="sxs-lookup"><span data-stu-id="6c121-161">assign the Reader role to the service principal</span></span>

<span data-ttu-id="6c121-162">다음 단계를 완료하려면 [OpenSSL](http://www.openssl.org/) 을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-162">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="6c121-163">자체 서명된 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-163">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="6c121-164">앞의 두 단계에서 2개의 파일 privkey.pem 및 cert.pem이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-164">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="6c121-165">공용 및 개인 키를 단일 파일로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-165">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="6c121-166">**examplecert.pem** 파일을 열고 **-----BEGIN CERTIFICATE-----**와 **-----END CERTIFICATE-----** 사이의 긴 시퀀스 문자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-166">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="6c121-167">인증서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-167">Copy the certificate data.</span></span> <span data-ttu-id="6c121-168">서비스 주체를 만들 때 이 데이터를 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-168">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="6c121-169">계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-169">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="6c121-170">서비스 주체를 만들려면 다음 명령과 같이 앱 이름과 인증서 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-170">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="6c121-171">새 서비스 주체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-171">The new service principal is returned.</span></span> <span data-ttu-id="6c121-172">사용 권한을 부여할 때 개체 ID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-172">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="6c121-173">로그인할 때 서비스 주체 이름으로 나열된 GUID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-173">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="6c121-174">이 GUID는 앱 ID와 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-174">This guid is the same value as the app id.</span></span> <span data-ttu-id="6c121-175">샘플 응용 프로그램에서 이 값을 클라이언트 ID라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-175">In the sample applications, this value is referred to as the Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="6c121-176">서비스 사용자에게 구독에 대한 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-176">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="6c121-177">이 예제에서는 구독에서 모든 리소스를 읽을 수 있는 권한이 부여된 읽기 권한자 역할에 서비스 주체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-177">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="6c121-178">다른 역할에 대해서는 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-178">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="6c121-179">objectid 매개 변수의 경우 응용 프로그램을 만들 때 사용한 개체 ID를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-179">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="6c121-180">이 명령을 실행하기 전에 새 서비스 주체가 Azure Active Directory 전체에 전파될 어느 정도의 시간을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-180">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="6c121-181">이러한 명령을 수동으로 실행할 때 작업 간에 충분 한 시간이 경과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-181">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="6c121-182">스크립트에 명령 사이에 절전 모드로 전환하는 단계를 추가해야 합니다(예시 `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="6c121-182">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="6c121-183">주체가 디렉터리에 존재하지 않는다는 오류가 표시되는 경우 명령을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-183">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="6c121-184">자동화된 Azure CLI 스크립트를 통해 인증서 제공</span><span class="sxs-lookup"><span data-stu-id="6c121-184">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="6c121-185">이제 응용 프로그램으로 로그인하여 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-185">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="6c121-186">서비스 주체로 로그인할 때마다 AD 앱에 디렉터리의 테넌트 ID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-186">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="6c121-187">테넌트는 Azure Active Directory의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-187">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="6c121-188">현재 인증된 구독에 대한 테넌트 ID를 검색하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-188">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="6c121-189">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-189">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="6c121-190">다른 구독의 테넌트 ID를 가져와야 하는 경우 다음 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-190">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="6c121-191">인증서 지문을 검색하고 불필요한 문자를 제거하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-191">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="6c121-192">다음과 유사한 지문 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-192">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="6c121-193">로그인에 사용할 클라이언트 ID를 검색해야 하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-193">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="6c121-194">로그인에 사용할 값은 서비스 주체 이름에 나열된 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-194">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="6c121-195">서비스 주체로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-195">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="6c121-196">이제 사용자는 작성한 Azure Active Directory 응용 프로그램에 대한 서비스 주체로 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-196">You are now authenticated as the service principal for the Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="6c121-197">자격 증명 변경</span><span class="sxs-lookup"><span data-stu-id="6c121-197">Change credentials</span></span>

<span data-ttu-id="6c121-198">보안 침해 또는 자격 증명 만료 때문에 AD 앱에 대한 자격 증명을 변경하려면 `azure ad app set`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-198">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="6c121-199">암호를 변경하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-199">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="6c121-200">인증서 값을 변경하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-200">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="6c121-201">디버그</span><span class="sxs-lookup"><span data-stu-id="6c121-201">Debug</span></span>

<span data-ttu-id="6c121-202">서비스 주체를 만들 때 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-202">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="6c121-203">**"Authentication_Unauthorized"** 또는 **"컨텍스트에서 구독을 찾을 수 없습니다."**</span><span class="sxs-lookup"><span data-stu-id="6c121-203">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="6c121-204">- 계정에 Azure Active Directory에서 앱을 등록하는 데 [필요한 권한](#required-permissions)이 없으면 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-204">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="6c121-205">일반적으로 Azure Active Directory의 관리 사용자만 앱을 등록할 수 있고 사용자 계정은 관리자가 아니면 이 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-205">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="6c121-206">관리자 역할에 사용자를 할당하거나 사용자가 앱을 등록할 수 있게 설정하도록 관리자에게 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-206">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="6c121-207">계정에 **"'/subscriptions/{guid}' 범위에 대해 'Microsoft.Authorization/roleAssignments/write' 작업을 수행할 수 있는 권한이 없습니다."** - 계정에 ID에 역할을 할당할 수 있는 충분한 권한이 없을 때 이 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="6c121-208">구독 관리자에게 사용자 액세스 관리자 역할에 사용자를 추가할 것을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="6c121-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="6c121-209">샘플 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="6c121-209">Sample applications</span></span>
<span data-ttu-id="6c121-210">다른 플랫폼을 통해 응용 프로그램으로 로그인하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-210">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="6c121-211">.NET</span><span class="sxs-lookup"><span data-stu-id="6c121-211">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="6c121-212">Java</span><span class="sxs-lookup"><span data-stu-id="6c121-212">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="6c121-213">Node.JS</span><span class="sxs-lookup"><span data-stu-id="6c121-213">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="6c121-214">Python</span><span class="sxs-lookup"><span data-stu-id="6c121-214">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="6c121-215">Ruby</span><span class="sxs-lookup"><span data-stu-id="6c121-215">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="6c121-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c121-216">Next steps</span></span>
* <span data-ttu-id="6c121-217">리소스 관리를 위해 Azure에 응용 프로그램을 통합하는 자세한 단계를 보려면 [Azure Resource Manager API를 사용한 권한 부여 개발자 가이드](resource-manager-api-authentication.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-217">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="6c121-218">인증서 및 Azure CLI 사용에 대한 자세한 내용은 [Linux 명령줄에서 Azure 서비스 보안 주체로 인증서 기반 인증](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-218">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="6c121-219">권한이 부여되거나 사용자에 대해 거부될 수 있는 작업 목록은 [Azure Resource Manager 리소스 공급자 작업](../active-directory/role-based-access-control-resource-provider-operations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c121-219">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
