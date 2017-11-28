---
title: "Azure Service Fabric 클러스터에 안전하게 연결 | Microsoft Docs"
description: "Service Fabric 클러스터에 대한 클라이언트 액세스를 인증하는 방법 및 클라이언트와 클러스터 간의 통신을 보호하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: d6a13ceb8ccd9207ecacc166247535d496d5dec7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="a5117-103">보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-103">Connect to a secure cluster</span></span>

<span data-ttu-id="a5117-104">클라이언트가 Service Fabric 클러스터 노드에 연결하는 경우 클라이언트는 인증서 보안 또는 Azure Active Directory(AAD)를 사용하여 인증을 받고 보안 통신이 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="a5117-105">이 인증을 통해 권한이 있는 사용자만 클러스터 및 배포된 응용 프로그램에 액세스할 수 있으며 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="a5117-106">인증서 또는 AAD 보안은 클러스터가 만들어지기 전에 클러스터에서 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span></span>  <span data-ttu-id="a5117-107">클러스터 보안 시나리오에 대한 자세한 내용은 [보안 클러스터](service-fabric-cluster-security.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5117-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="a5117-108">인증서로 보호되는 클러스터에 연결하는 경우 클러스터에 연결할 컴퓨터에서 [클라이언트 인증서를 설정](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert)하세요.</span><span class="sxs-lookup"><span data-stu-id="a5117-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="a5117-109">Azure Service Fabric CLI(sfctl)를 사용하여 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-109">Connect to a secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="a5117-110">몇 가지 방법으로 Service Fabric CLI(sfctl)를 사용하는 보안 클러스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-110">There are a few different ways to connect to a secure cluster using the Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="a5117-111">인증에 클라이언트 인증서를 사용하는 경우 인증서 세부 정보는 클러스터 노드에 배포된 인증서와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-111">When using a client certificate for authentication, the certificate details must match a certificate deployed to the cluster nodes.</span></span> <span data-ttu-id="a5117-112">인증서에 CA(인증 기관)가 있으면 신뢰할 수 있는 CA를 추가적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-112">If your certificate has Certificate Authorities (CAs), you need to additionally specify the trusted CAs.</span></span>

<span data-ttu-id="a5117-113">`sfctl cluster select` 명령을 사용하여 클러스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-113">You can connect to a cluster using the `sfctl cluster select` command.</span></span>

<span data-ttu-id="a5117-114">클라이언트 인증서는 인증서 및 키 쌍 또는 단일 pem 파일이라는 두 가지 형태로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="a5117-115">암호로 보호되는 `pem` 파일의 경우 암호를 입력하라는 메시지가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-115">For password protected `pem` files, you will be prompted automatically to enter the password.</span></span>

<span data-ttu-id="a5117-116">클라이언트 인증서를 pem 파일로 지정하려면 `--pem` 인수에 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-116">To specify the client certificate as a pem file, specify the file path in the `--pem` argument.</span></span> <span data-ttu-id="a5117-117">예:</span><span class="sxs-lookup"><span data-stu-id="a5117-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="a5117-118">명령을 실행하기 전에 암호로 보호되는 pem 파일에 암호를 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-118">Password protected pem files will prompt for password prior to running any command.</span></span>

<span data-ttu-id="a5117-119">인증서, 키 쌍을 지정하려면 `--cert` 및 `--key` 인수를 사용하여 각 파일에 대한 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-119">To specify a cert, key pair use the `--cert` and `--key` arguments to specify the file paths to each respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="a5117-120">경우에 따라 테스트 또는 개발 클러스터 보안에 사용된 인증서가 인증서 유효성 검사에 실패하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-120">Sometimes certificates used to secure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="a5117-121">인증서 유효성 검사를 무시하려면 `--no-verify` 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-121">To bypass certificate verification, specify the `--no-verify` option.</span></span> <span data-ttu-id="a5117-122">예:</span><span class="sxs-lookup"><span data-stu-id="a5117-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="a5117-123">프로덕션 Service Fabric 클러스터에 연결할 때 `no-verify` 옵션을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a5117-123">Do not use the `no-verify` option when connecting to production Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="a5117-124">또한 신뢰할 수 있는 CA 인증서 또는 개별 인증서의 디렉터리 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-124">In addition, you can specify paths to directories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="a5117-125">이러한 경로를 지정하려면 `--ca` 인수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-125">To specify these paths, use the `--ca` argument.</span></span> <span data-ttu-id="a5117-126">예:</span><span class="sxs-lookup"><span data-stu-id="a5117-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="a5117-127">연결 후에는 클러스터와 상호 작용하기 위해 [다른 sfctl 명령을 실행](service-fabric-cli.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-127">After you connect, you should be able to [run other sfctl commands](service-fabric-cli.md) to interact with the cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a><span data-ttu-id="a5117-128">PowerShell을 사용하여 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-128">Connect to a cluster using PowerShell</span></span>
<span data-ttu-id="a5117-129">PowerShell을 통해 클러스터에서 작업을 수행하기 전에 먼저 클러스터와 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-129">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span></span> <span data-ttu-id="a5117-130">클러스터 연결은 지정된 PowerShell 세션에서 모든 후속 명령에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-130">The cluster connection is used for all subsequent commands in the given PowerShell session.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="a5117-131">비보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-131">Connect to an unsecure cluster</span></span>

<span data-ttu-id="a5117-132">비보안 클러스터에 연결하려면 **Connect-ServiceFabricCluster** 명령에 클러스터 끝점 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-132">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="a5117-133">Azure Active Directory를 사용하여 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-133">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="a5117-134">클러스터 관리자 액세스 권한을 부여하기 위해 Azure Active Directory를 사용하는 보안 클러스터에 연결하려면 클러스터 인증서 지문을 제공하고 *AzureActiveDirectory* 플래그를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-134">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="a5117-135">클라이언트 인증서를 사용하여 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-135">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="a5117-136">다음 PowerShell 명령을 실행하여 관리자 액세스 권한을 부여하는 데 클라이언트 인증서를 사용하는 보안 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-136">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span></span> <span data-ttu-id="a5117-137">클러스터 관리에 대한 권한이 부여된 클러스터 인증서 지문과 클라이언트 인증서 지문을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-137">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="a5117-138">인증서 세부 정보는 클러스터 노드의 인증서와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-138">The certificate details must match a certificate on the cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="a5117-139">*ServerCertThumbprint* 는 클러스터 노드에 설치된 서버 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-139">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span></span> <span data-ttu-id="a5117-140">*FindValue* 는 관리자 클라이언트 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-140">*FindValue* is the thumbprint of the admin client certificate.</span></span>
<span data-ttu-id="a5117-141">매개 변수가 입력되면 명령은 다음 예와 같아집니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-141">When the parameters are filled in, the command looks like the following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="a5117-142">Windows Active Directory를 사용하여 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-142">Connect to a secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="a5117-143">독립 실행형 클러스터가 AD 보안을 사용하여 배포되는 경우 "WindowsCredential" 스위치를 추가하여 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-143">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a><span data-ttu-id="a5117-144">FabricClient API를 사용하여 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-144">Connect to a cluster using the FabricClient APIs</span></span>
<span data-ttu-id="a5117-145">Service Fabric SDK는 클러스터 관리를 위해 [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-145">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="a5117-146">FabricClient API를 사용하려면 Microsoft.ServiceFabric NuGet 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-146">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="a5117-147">비보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-147">Connect to an unsecure cluster</span></span>

<span data-ttu-id="a5117-148">원격 비보안 클러스터에 연결하려면 FabricClient 인스턴스를 만들고 클러스터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-148">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="a5117-149">클러스터 내에서 실행되는 코드(예를 들어 Reliable Service에서)의 경우 클러스터 주소를 지정하지 *않고* FabricClient를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span></span> <span data-ttu-id="a5117-150">FabricClient는 현재 코드가 실행 중인 노드의 로컬 관리 게이트웨이로 연결되어 추가 네트워크 홉이 방지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-150">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="a5117-151">클라이언트 인증서를 사용하여 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-151">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="a5117-152">클러스터의 노드에는 해당 일반 이름 또는 SAN의 DNS 이름이 [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient)에 설정된 [RemoteCommonNames 속성](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames)에 표시되는 유효한 인증서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-152">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="a5117-153">이 과정에 따라 클라이언트와 클러스터 노드 간 상호 인증이 가능해집니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-153">Following this process enables mutual authentication between the client and the cluster nodes.</span></span>

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="a5117-154">Azure Active Directory를 사용하여 대화형으로 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-154">Connect to a secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="a5117-155">다음 예제에서는 클라이언트 ID에는 Azure Active Directory를, 서버 ID에는 서버 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-155">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="a5117-156">클러스터를 연결할 때는 대화형 로그인을 위한 대화 상자 창이 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-156">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="a5117-157">Azure Active Directory를 사용하여 비대화형으로 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-157">Connect to a secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="a5117-158">다음 예제에서는 Microsoft.IdentityModel.Clients.ActiveDirectory 버전 2.19.208020213을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-158">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="a5117-159">AAD 토큰 획득에 대한 자세한 내용은 [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5117-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="a5117-160">사전 메타데이터 지식 없이 Azure Active Directory를 사용하여 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-160">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="a5117-161">다음 예제에서는 비대화형 토큰 획득을 사용하지만 사용자 지정 대화형 토큰 획득 환경을 빌드하는 데 동일한 접근 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-161">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span></span> <span data-ttu-id="a5117-162">토큰 획득에 필요한 Azure Active Directory 메타데이터는 클러스터 구성에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-162">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="a5117-163">Service Fabric Explorer를 사용하여 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-163">Connect to a secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="a5117-164">지정된 클러스터를 위한 [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)에 도달하려면 브라우저를 다음으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-164">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="a5117-165">전체 URL은 Azure 포털의 클러스터 필수 창에서도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-165">The full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="a5117-166">Azure Active Directory를 사용하여 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-166">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="a5117-167">AAD로 보호되는 클러스터에 연결하려면 브라우저를 다음으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-167">To connect to a cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="a5117-168">AAD에 로그인하라는 메시지가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-168">You are automatically be prompted to log in with AAD.</span></span>

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="a5117-169">클라이언트 인증서를 사용하여 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="a5117-169">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="a5117-170">인증서로 보호되는 클러스터에 연결하려면 브라우저를 다음으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-170">To connect to a cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="a5117-171">클라이언트 인증서를 선택하라는 메시지가 자동으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-171">You are automatically be prompted to select a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a><span data-ttu-id="a5117-172">원격 컴퓨터에서 클라이언트 인증서 설정</span><span class="sxs-lookup"><span data-stu-id="a5117-172">Set up a client certificate on the remote computer</span></span>
<span data-ttu-id="a5117-173">클러스터를 보호하려면 적어도 두 개의 인증서(클러스터와 서버 인증서용 한 개 및 클라이언트 액세스용 또 한 개)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-173">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="a5117-174">추가 보조 인증서와 클라이언트 액세스 인증서도 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="a5117-175">인증서 보안을 사용하여 클라이언트와 클러스터 노드 간 통신을 보호하려면 먼저 클라이언트 인증서를 획득하고 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-175">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span></span> <span data-ttu-id="a5117-176">인증서는 로컬 컴퓨터의 개인(내) 저장소 또는 현재 사용자의 개인 저장소에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-176">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span></span>  <span data-ttu-id="a5117-177">클라이언트가 클러스터를 인증할 수 있도록 하려면 서버 인증서의 지문도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-177">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span></span>

<span data-ttu-id="a5117-178">다음 PowerShell cmdlet을 실행하여 클러스터에 액세스하는 데 사용하는 컴퓨터에서 클라이언트 인증서를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-178">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="a5117-179">자체 서명된 인증서는 사용 중인 컴퓨터의 "신뢰할 수 있는 사용자" 저장소로 가져와야 보안 클러스터에 연결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5117-179">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="a5117-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5117-180">Next steps</span></span>

* [<span data-ttu-id="a5117-181">서비스 패브릭 클러스터 업그레이드 프로세스 및 사용자 기대 수준</span><span class="sxs-lookup"><span data-stu-id="a5117-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="a5117-182">Visual Studio에서 서비스 패브릭 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="a5117-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="a5117-183">서비스 패브릭 상태 모델 소개</span><span class="sxs-lookup"><span data-stu-id="a5117-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="a5117-184">응용 프로그램 보안 및 RunAs</span><span class="sxs-lookup"><span data-stu-id="a5117-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="a5117-185">Service Fabric CLI 시작</span><span class="sxs-lookup"><span data-stu-id="a5117-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
