---
title: "Service Fabric 응용 프로그램에서 비밀 관리 | Microsoft Docs"
description: "이 문서에서는 서비스 패브릭 응용 프로그램에서 비밀 값을 보호하는 방법에 대해 설명합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: d71924cda8bb3bffbe221946d80dba150359e38e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="5d7d1-103">서비스 패브릭 응용 프로그램의 비밀 관리</span><span class="sxs-lookup"><span data-stu-id="5d7d1-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="5d7d1-104">이 가이드에서는 서비스 패브릭 응용 프로그램에서 비밀을 관리하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-104">This guide walks you through the steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="5d7d1-105">저장소 연결 문자열, 암호, 일반 텍스트로 처리하면 안 되는 값 등 모든 민감한 정보를 비밀로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="5d7d1-106">이 가이드에서는 Azure 주요 자격 증명 모음을 사용하여 키와 비밀을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-106">This guide uses Azure Key Vault to manage keys and secrets.</span></span> <span data-ttu-id="5d7d1-107">하지만 응용 프로그램에서 비밀을 *사용* 하는 것은 클라우드 플랫폼에 구애를 받지 않으므로 그 어디에 호스트된 클러스터에도 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-107">However, *using* secrets in an application is cloud platform-agnostic to allow applications to be deployed to a cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="5d7d1-108">개요</span><span class="sxs-lookup"><span data-stu-id="5d7d1-108">Overview</span></span>
<span data-ttu-id="5d7d1-109">[서비스 구성 패키지][config-package]를 통해 서비스 구성 설정을 관리하는 방법이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-109">The recommended way to manage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="5d7d1-110">구성 패키지는 관리되는 상태 유효성 검사 및 자동 롤백을 사용하여 롤링 업그레이드를 통해 버전이 관리되며 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="5d7d1-111">이 방법은 전역 서비스 중단 가능성을 줄이기 때문에 기본 설정으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-111">This is preferred to global configuration as it reduces the chances of a global service outage.</span></span> <span data-ttu-id="5d7d1-112">암호화된 비밀도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="5d7d1-113">서비스 패브릭에는 인증서 암호화를 사용하여 구성 패키지 Settings.xml 파일의 값을 암호화 및 해독하는 기본 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="5d7d1-114">다음 다이어그램은 서비스 패브릭 응용 프로그램에서 비밀 관리가 이루어지는 기본 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-114">The following diagram illustrates the basic flow for secret management in a Service Fabric application:</span></span>

![비밀 관리 개요][overview]

<span data-ttu-id="5d7d1-116">이 흐름은 주요 네 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="5d7d1-117">데이터 암호화 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="5d7d1-118">클러스터에 인증서를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-118">Install the certificate in your cluster.</span></span>
3. <span data-ttu-id="5d7d1-119">인증서를 사용하여 응용 프로그램을 배포할 때 비밀 값을 암호화하여 서비스의 Settings.xml 구성 파일에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-119">Encrypt secret values when deploying an application with the certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="5d7d1-120">동일한 암호화 인증서로 암호를 해독하여 Settings.xml 파일에서 암호화된 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-120">Read encrypted values out of Settings.xml by decrypting with the same encipherment certificate.</span></span> 

<span data-ttu-id="5d7d1-121">[Azure Key Vault][key-vault-get-started]는 인증서에 대한 안전한 저장소 위치이자 Azure의 Service Fabric 클러스터에 설치된 인증서를 가져오는 수단으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way to get certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="5d7d1-122">Azure에 배포하지 않는 경우 서비스 패브릭 응용 프로그램의 비밀을 관리하기 위해 주요 자격 증명 모음을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-122">If you are not deploying to Azure, you do not need to use Key Vault to manage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="5d7d1-123">데이터 암호화 인증서</span><span class="sxs-lookup"><span data-stu-id="5d7d1-123">Data encipherment certificate</span></span>
<span data-ttu-id="5d7d1-124">데이터 암호화 인증서는 서비스에 포함된 Settings.xml의 구성 값을 암호화하고 해독하는 용도로만 엄격하게 사용되며 암호화 텍스트의 인증에는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="5d7d1-125">인증서는 다음 요구 사항을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-125">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="5d7d1-126">인증서에 개인 키가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-126">The certificate must contain a private key.</span></span>
* <span data-ttu-id="5d7d1-127">개인 정보 교환(.pfx) 파일로 내보낼 수 있는 키 교환용 인증서를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-127">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="5d7d1-128">인증서 키 사용에는 데이터 암호화(10)가 포함되어야 하며, 서버 인증 또는 클라이언트 인증은 포함되면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-128">The certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="5d7d1-129">예를 들어 PowerShell을 사용하여 자체 서명된 인증서를 만들 때 `KeyUsage` 플래그가 `DataEncipherment`로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-129">For example, when creating a self-signed certificate using PowerShell, the `KeyUsage` flag must be set to `DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-the-certificate-in-your-cluster"></a><span data-ttu-id="5d7d1-130">클러스터에 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="5d7d1-130">Install the certificate in your cluster</span></span>
<span data-ttu-id="5d7d1-131">클러스터의 각 노드에 이 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-131">This certificate must be installed on each node in the cluster.</span></span> <span data-ttu-id="5d7d1-132">이 인증서는 런타임에 서비스의 Settings.xml에 저장된 값을 해독하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-132">It will be used at runtime to decrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="5d7d1-133">설정 지침은 [Azure Resource Manager를 사용하여 클러스터를 만드는 방법][service-fabric-cluster-creation-via-arm]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-133">See [how to create a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="5d7d1-134">응용 프로그램 비밀 암호화</span><span class="sxs-lookup"><span data-stu-id="5d7d1-134">Encrypt application secrets</span></span>
<span data-ttu-id="5d7d1-135">서비스 패브릭 SDK는 비밀 암호화 및 암호 해독 기능이 기본적으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-135">The Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="5d7d1-136">작성 시 비밀 값을 암호화한 후 서비스 코드에서 프로그래밍 방식으로 해독하여 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="5d7d1-137">다음 PowerShell 명령은 비밀을 암호화하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-137">The following PowerShell command is used to encrypt a secret.</span></span> <span data-ttu-id="5d7d1-138">이 명령은 값을 암호화합니다. 암호화 텍스트에 서명하지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-138">This command only encrypts the value; it does **not** sign the cipher text.</span></span> <span data-ttu-id="5d7d1-139">클러스터에 설치된 것과 동일한 암호화 인증서를 사용하여 비밀 값의 암호 텍스트를 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-139">You must use the same encipherment certificate that is installed in your cluster to produce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="5d7d1-140">그 결과로 얻게 되는 Base-64 문자열에는 비밀 암호 텍스트와 암호화에 사용된 인증서에 대한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-140">The resulting base-64 string contains both the secret ciphertext as well as information about the certificate that was used to encrypt it.</span></span>  <span data-ttu-id="5d7d1-141">Base-64로 인코딩된 문자열은 서비스의 `IsEncrypted` 특성이 `true`로 설정된 Settings.xml 구성 파일의 매개 변수에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-141">The base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with the `IsEncrypted` attribute set to `true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="5d7d1-142">응용 프로그램 비밀을 응용 프로그램 인스턴스에 삽입</span><span class="sxs-lookup"><span data-stu-id="5d7d1-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="5d7d1-143">여러 환경에 배포할 때에는 배포를 최대한 자동화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-143">Ideally, deployment to different environments should be as automated as possible.</span></span> <span data-ttu-id="5d7d1-144">빌드 환경에서 비밀 암호화를 수행하고 응용 프로그램 인스턴스를 만들 때 암호화된 비밀을 매개 변수로 제공하면 배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-144">This can be accomplished by performing secret encryption in a build environment and providing the encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="5d7d1-145">Settings.xml에 재정의 가능한 매개 변수 사용</span><span class="sxs-lookup"><span data-stu-id="5d7d1-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="5d7d1-146">Settings.xml 구성 파일은 응용 프로그램 생성 시 제공할 수 있는 재정의 가능한 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-146">The Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="5d7d1-147">매개 변수 값을 입력하는 대신 `MustOverride` 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-147">Use the `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="5d7d1-148">Settings.xml의 값을 재정의하려면 ApplicationManifest.xml에서 서비스의 재정의 매개 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-148">To override values in Settings.xml, declare an override parameter for the service in ApplicationManifest.xml:</span></span>

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

<span data-ttu-id="5d7d1-149">이제 응용 프로그램의 인스턴스를 만들 때 이 값을 *응용 프로그램 매개 변수* 로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-149">Now the value can be specified as an *application parameter* when creating an instance of the application.</span></span> <span data-ttu-id="5d7d1-150">응용 프로그램 인스턴스 만들기를 PowerShell로 스크립팅하거나 C#으로 작성하면 빌드 프로세스에 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="5d7d1-151">PowerShell을 사용하면 매개 변수가 `New-ServiceFabricApplication` 명령에 [해시 테이블](https://technet.microsoft.com/library/ee692803.aspx)로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-151">Using PowerShell, the parameter is supplied to the `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="5d7d1-152">C#을 사용하면 응용 프로그램 매개 변수가 `ApplicationDescription`에 `NameValueCollection`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="5d7d1-153">서비스 코드에서 비밀 해독</span><span class="sxs-lookup"><span data-stu-id="5d7d1-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="5d7d1-154">서비스 패브릭의 서비스는 기본적으로 Windows의 네트워크 서비스에서 실행되며 추가 설정 없이는 노드에 설치된 인증서에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access to certificates installed on the node without some extra setup.</span></span>

<span data-ttu-id="5d7d1-155">데이터 암호화 인증서를 사용할 때에는 네트워크 서비스 또는 서비스가 실행되고 있는 사용자 계정이 인증서의 개인 키에 액세스할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-155">When using a data encipherment certificate, you need to make sure NETWORK SERVICE or whatever user account the service is running under has access to the certificate's private key.</span></span> <span data-ttu-id="5d7d1-156">서비스 패브릭이 서비스에 대한 액세스 권한을 자동으로 부여하도록 구성하면 자동으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-156">Service Fabric will handle granting access for your service automatically if you configure it to do so.</span></span> <span data-ttu-id="5d7d1-157">이 구성은 ApplicationManifest.xml에서 인증서의 사용자 및 보안 정책을 정의하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="5d7d1-158">다음은 지문을 통해 정의된 인증서에 대한 읽기 권한을 네트워크 서비스 계정에 부여하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-158">In the following example, the NETWORK SERVICE account is given read access to a certificate defined by its thumbprint:</span></span>

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> <span data-ttu-id="5d7d1-159">Windows의 인증서 저장소 스냅인에서 인증서 지문을 복사하는 경우 지문 문자열의 시작 부분에 보이지 않는 문자가 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-159">When copying a certificate thumbprint from the certificate store snap-in on Windows, an invisible character is placed at the beginning of the thumbprint string.</span></span> <span data-ttu-id="5d7d1-160">이 보이지 않는 문자는 지문으로 인증서를 찾으려 할 때 오류를 일으킬 수 있으므로 이 추가 문자를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-160">This invisible character can cause an error when trying to locate a certificate by thumbprint, so be sure to delete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="5d7d1-161">서비스 코드에 응용 프로그램 암호 사용</span><span class="sxs-lookup"><span data-stu-id="5d7d1-161">Use application secrets in service code</span></span>
<span data-ttu-id="5d7d1-162">구성 패키지의 Settings.xml에서 구성 값에 액세스할 수 있는 API를 사용하면 `IsEncrypted` 특성이 `true`로 설정된 값을 간단하게 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-162">The API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have the `IsEncrypted` attribute set to `true`.</span></span> <span data-ttu-id="5d7d1-163">암호화된 텍스트에는 암호화에 사용된 인증서 정보가 포함되어 있으므로 수동으로 인증서를 찾을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-163">Since the encrypted text contains information about the certificate used for encryption, you do not need to manually find the certificate.</span></span> <span data-ttu-id="5d7d1-164">서비스가 실행되고 있는 노드에 인증서를 설치하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-164">The certificate just needs to be installed on the node that the service is running on.</span></span> <span data-ttu-id="5d7d1-165">간단하게 `DecryptValue()` 메서드를 호출하여 원래 비밀 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7d1-165">Simply call the `DecryptValue()` method to retrieve the original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="5d7d1-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5d7d1-166">Next Steps</span></span>
<span data-ttu-id="5d7d1-167">[다양한 보안 권한으로 응용 프로그램 실행](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="5d7d1-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
