---
title: "aaaConnect tooan Azure 서비스 패브릭 클러스터에 안전 하 게 | Microsoft Docs"
description: "고 tooauthenticate 클라이언트 tooa 서비스 패브릭 클러스터에 액세스 하는 방법 설명 클라이언트와 클러스터 간의 toosecure 통신 합니다."
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
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="b01e2-103">Tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-103">Connect tooa secure cluster</span></span>

<span data-ttu-id="b01e2-104">클라이언트가 tooa 서비스 패브릭 클러스터 노드를 연결 하는 경우 hello 클라이언트에 인증 하 고 안전한 통신이 인증서 보안 또는 Azure Active Directory (AAD)를 사용 하 여 설정 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-104">When a client connects tooa Service Fabric cluster node, hello client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="b01e2-105">이 인증 권한이 있는 사용자만 hello 클러스터에 액세스할 수 응용 프로그램을 배포 및 관리 작업을 수행 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-105">This authentication ensures that only authorized users can access hello cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="b01e2-106">인증서 또는 AAD 보안 된 이전에 설정한 상태 여야 hello 클러스터에서 hello 클러스터를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="b01e2-106">Certificate or AAD security must have been previously enabled on hello cluster when hello cluster was created.</span></span>  <span data-ttu-id="b01e2-107">클러스터 보안 시나리오에 대한 자세한 내용은 [보안 클러스터](service-fabric-cluster-security.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b01e2-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="b01e2-108">인증서를 사용 하 여 보호 tooa 클러스터를 연결 하는 경우 [hello 클라이언트 인증서를 설정](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) toohello 클러스터를 연결 하는 hello 컴퓨터에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-108">If you are connecting tooa cluster secured with certificates, [set up hello client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on hello computer that connects toohello cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="b01e2-109">Azure 서비스 패브릭 CLI (sfctl)를 사용 하 여 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-109">Connect tooa secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="b01e2-110">몇 가지 방법으로 tooconnect tooa 보안 클러스터 서비스 패브릭 CLI (sfctl) hello를 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-110">There are a few different ways tooconnect tooa secure cluster using hello Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="b01e2-111">클라이언트 인증서를 인증에 대 한을 사용할 때는 hello 인증서 세부 정보에는 인증서와 일치 해야 toohello 클러스터 노드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-111">When using a client certificate for authentication, hello certificate details must match a certificate deployed toohello cluster nodes.</span></span> <span data-ttu-id="b01e2-112">Tooadditionally 필요한 인증서 인증 기관 (Ca)가 있으면 hello Ca를 신뢰할 수 있는 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-112">If your certificate has Certificate Authorities (CAs), you need tooadditionally specify hello trusted CAs.</span></span>

<span data-ttu-id="b01e2-113">Hello를 사용 하 여 tooa 클러스터를 연결할 수 있습니다 `sfctl cluster select` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-113">You can connect tooa cluster using hello `sfctl cluster select` command.</span></span>

<span data-ttu-id="b01e2-114">클라이언트 인증서는 인증서 및 키 쌍 또는 단일 pem 파일이라는 두 가지 형태로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="b01e2-115">암호로 보호에 대 한 `pem` 파일 됩니다 tooenter hello 암호 라는 메시지가 자동으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-115">For password protected `pem` files, you will be prompted automatically tooenter hello password.</span></span>

<span data-ttu-id="b01e2-116">hello에 hello 파일 경로 지정 하는 pem 파일로 toospecify hello 클라이언트 인증서 `--pem` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-116">toospecify hello client certificate as a pem file, specify hello file path in hello `--pem` argument.</span></span> <span data-ttu-id="b01e2-117">예:</span><span class="sxs-lookup"><span data-stu-id="b01e2-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="b01e2-118">암호로 보호 된 pem 파일 이전 toorunning 암호에 대 한 모든 명령을 라는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-118">Password protected pem files will prompt for password prior toorunning any command.</span></span>

<span data-ttu-id="b01e2-119">toospecify 인증서, 키 쌍 사용 하 여 hello `--cert` 및 `--key` toospecify hello 파일 경로 tooeach 각 파일 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-119">toospecify a cert, key pair use hello `--cert` and `--key` arguments toospecify hello file paths tooeach respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="b01e2-120">인증서 toosecure 테스트를 사용 하는 경우에 따라 또는 dev 클러스터 인증서 유효성 검사에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-120">Sometimes certificates used toosecure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="b01e2-121">인증서를 확인, toobypass hello 지정 `--no-verify` 옵션.</span><span class="sxs-lookup"><span data-stu-id="b01e2-121">toobypass certificate verification, specify hello `--no-verify` option.</span></span> <span data-ttu-id="b01e2-122">예:</span><span class="sxs-lookup"><span data-stu-id="b01e2-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="b01e2-123">Hello를 사용 하지 마십시오 `no-verify` 옵션 tooproduction 서비스 패브릭 클러스터를 연결 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="b01e2-123">Do not use hello `no-verify` option when connecting tooproduction Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="b01e2-124">또한 신뢰할 수 있는 CA 인증서 또는 개별 인증서의 경로 toodirectories를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-124">In addition, you can specify paths toodirectories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="b01e2-125">toospecify hello를 사용 하 여 이러한 경로 `--ca` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-125">toospecify these paths, use hello `--ca` argument.</span></span> <span data-ttu-id="b01e2-126">예:</span><span class="sxs-lookup"><span data-stu-id="b01e2-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="b01e2-127">연결 된 후 있어야 너무[다른 sfctl 명령을 실행할](service-fabric-cli.md) hello 클러스터와 toointeract 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-127">After you connect, you should be able too[run other sfctl commands](service-fabric-cli.md) toointeract with hello cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a><span data-ttu-id="b01e2-128">PowerShell을 사용 하 여 tooa 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-128">Connect tooa cluster using PowerShell</span></span>
<span data-ttu-id="b01e2-129">PowerShell 통해 클러스터에 대 한 작업을 수행 하기 전에 먼저 연결 toohello 클러스터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-129">Before you perform operations on a cluster through PowerShell, first establish a connection toohello cluster.</span></span> <span data-ttu-id="b01e2-130">hello 클러스터 연결 PowerShell 세션을 제공 하는 hello에 있는 모든 후속 명령에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-130">hello cluster connection is used for all subsequent commands in hello given PowerShell session.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="b01e2-131">Tooan 보안 되지 않은 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-131">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="b01e2-132">보안 되지 않은 tooconnect tooan 클러스터, 클러스터 끝점 주소 toohello hello 제공 **Connect-servicefabriccluster** 명령:</span><span class="sxs-lookup"><span data-stu-id="b01e2-132">tooconnect tooan unsecure cluster, provide hello cluster endpoint address toohello **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="b01e2-133">Azure Active Directory를 사용 하 여 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-133">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="b01e2-134">Azure Active Directory tooauthorize 클러스터 관리자 액세스를 사용 하는 tooconnect tooa 보안 클러스터 hello 클러스터 인증서 지문을 제공 및 hello를 사용 하 여 *AzureActiveDirectory* 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-134">tooconnect tooa secure cluster that uses Azure Active Directory tooauthorize cluster administrator access, provide hello cluster certificate thumbprint and use hello *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="b01e2-135">클라이언트 인증서를 사용 하 여 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-135">Connect tooa secure cluster using a client certificate</span></span>
<span data-ttu-id="b01e2-136">다음 PowerShell 명령을 tooconnect tooa 보안 클러스터 실행된 hello 클라이언트 인증서 tooauthorize 관리자 액세스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-136">Run hello following PowerShell command tooconnect tooa secure cluster that uses client certificates tooauthorize administrator access.</span></span> <span data-ttu-id="b01e2-137">Hello 클러스터 인증서 지문 및 클러스터 관리에 대 한 권한을 부여 받은 hello 클라이언트 인증서의 지문 hello 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-137">Provide hello cluster certificate thumbprint and hello thumbprint of hello client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="b01e2-138">hello 인증서 세부 정보는 hello 클러스터 노드에서 인증서를 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-138">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="b01e2-139">*ServerCertThumbprint* is hello 클러스터 노드에 설치 되어 hello 서버 인증서의 지문 안녕하세요.</span><span class="sxs-lookup"><span data-stu-id="b01e2-139">*ServerCertThumbprint* is hello thumbprint of hello server certificate installed on hello cluster nodes.</span></span> <span data-ttu-id="b01e2-140">*FindValue* hello 관리 클라이언트 인증서의 지문 안녕하세요 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-140">*FindValue* is hello thumbprint of hello admin client certificate.</span></span>
<span data-ttu-id="b01e2-141">Hello 매개 변수 가득 차면 hello 명령은 다음 예제는 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-141">When hello parameters are filled in, hello command looks like hello following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="b01e2-142">Windows Active Directory를 사용 하 여 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-142">Connect tooa secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="b01e2-143">AD 보안을 사용 하 여 독립 실행형 클러스터를 배포한 경우 hello 스위치 "WindowsCredential"를 추가 하 여 toohello 클러스터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-143">If your standalone cluster is deployed using AD security, connect toohello cluster by appending hello switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a><span data-ttu-id="b01e2-144">Hello FabricClient Api를 사용 하 여 tooa 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-144">Connect tooa cluster using hello FabricClient APIs</span></span>
<span data-ttu-id="b01e2-145">서비스 패브릭 SDK hello 제공 hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) 클러스터 관리를 위한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-145">hello Service Fabric SDK provides hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="b01e2-146">toouse hello를 FabricClient Api hello를 Microsoft.ServiceFabric NuGet 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-146">toouse hello FabricClient APIs, get hello Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="b01e2-147">Tooan 보안 되지 않은 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-147">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="b01e2-148">tooconnect tooa 원격 보안 되지 않은 클러스터 FabricClient 인스턴스를 만들고 hello 클러스터 주소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-148">tooconnect tooa remote unsecured cluster, create a FabricClient instance and provide hello cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="b01e2-149">클러스터 내에서 실행 되는 코드에 대 한 예를 들어 신뢰할 수 있는 서비스를 만듭니다는 FabricClient *없이* hello 클러스터 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying hello cluster address.</span></span> <span data-ttu-id="b01e2-150">FabricClient toohello 로컬 관리 연결 hello 노드 hello 코드에서 게이트웨이 현재 실행 되 고, 추가로 네트워크 홉을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-150">FabricClient connects toohello local management gateway on hello node hello code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="b01e2-151">클라이언트 인증서를 사용 하 여 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-151">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="b01e2-152">hello 클러스터의 노드 hello에 유효한 인증서 일반 이름이 또는 있어야 hello에 SAN에 DNS 이름이 나타납니다 [RemoteCommonNames 속성](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) 에 설정 [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient)합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-152">hello nodes in hello cluster must have valid certificates whose common name or DNS name in SAN appears in hello [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="b01e2-153">이 프로세스 hello 클라이언트와 hello 클러스터 노드 간의 상호 인증을 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-153">Following this process enables mutual authentication between hello client and hello cluster nodes.</span></span>

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="b01e2-154">Azure Active Directory를 사용 하 여 대화형으로 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-154">Connect tooa secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="b01e2-155">다음 예제에서는 Azure Active Directory 클라이언트 id 및 서버에 대 한 인증서 서버 id 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-155">hello following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="b01e2-156">대화 상자 창이 자동으로 팝업 대화형 로그인에 대해 toohello 클러스터를 연결 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-156">A dialog window automatically pops up for interactive sign-in upon connecting toohello cluster.</span></span>

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="b01e2-157">Azure Active Directory를 사용 하 여 비 대화형 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-157">Connect tooa secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="b01e2-158">hello 다음 예제에서는 의존 Microsoft.IdentityModel.Clients.ActiveDirectory, 버전: 2.19.208020213 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-158">hello following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="b01e2-159">AAD 토큰 획득에 대한 자세한 내용은 [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b01e2-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="b01e2-160">Azure Active Directory를 사용 하 여 이전 메타 데이터 지식 없이도 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-160">Connect tooa secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="b01e2-161">hello 다음 예제에서는 비 대화형 토큰 획득 하지만 hello 같은 방법을 수 사용된 toobuild 대화형 사용자 지정 토큰 획득 환경.</span><span class="sxs-lookup"><span data-stu-id="b01e2-161">hello following example uses non-interactive token acquisition, but hello same approach can be used toobuild a custom interactive token acquisition experience.</span></span> <span data-ttu-id="b01e2-162">클러스터 구성에서 토큰 획득 필요한 hello Azure Active Directory 메타 데이터는 읽기입니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-162">hello Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="b01e2-163">서비스 패브릭 탐색기를 사용 하 여 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-163">Connect tooa secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="b01e2-164">tooreach [서비스 패브릭 탐색기](service-fabric-visualizing-your-cluster.md) 특정된 클러스터에 대 한 브라우저를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="b01e2-165">hello 전체 URL도 hello Azure 포털의 hello 클러스터 essentials 창에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-165">hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="b01e2-166">Azure Active Directory를 사용 하 여 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-166">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="b01e2-167">tooconnect tooa 클러스터 AAD를 사용 하 여 보호 되는 브라우저를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-167">tooconnect tooa cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="b01e2-168">자동으로 AAD 사용 하 여 증명된 toolog 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-168">You are automatically be prompted toolog in with AAD.</span></span>

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="b01e2-169">클라이언트 인증서를 사용 하 여 tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="b01e2-169">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="b01e2-170">인증서를 사용 하 여 보호 되는 tooconnect tooa 클러스터 브라우저를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-170">tooconnect tooa cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="b01e2-171">증명된 tooselect 클라이언트 인증서를 자동으로 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-171">You are automatically be prompted tooselect a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a><span data-ttu-id="b01e2-172">Hello 원격 컴퓨터에 클라이언트 인증서를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-172">Set up a client certificate on hello remote computer</span></span>
<span data-ttu-id="b01e2-173">두 개 이상의 인증서 hello 클러스터 hello 클러스터와 서버 인증서에 대 한 및 클라이언트 액세스 관리를 위한 보안에 사용할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-173">At least two certificates should be used for securing hello cluster, one for hello cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="b01e2-174">추가 보조 인증서와 클라이언트 액세스 인증서도 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="b01e2-175">클라이언트와 사용 하 여 클러스터 노드 간의 toosecure hello 통신 보안 인증서, 먼저 tooobtain 필요 하 고 hello 클라이언트 인증서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-175">toosecure hello communication between a client and a cluster node using certificate security, you first need tooobtain and install hello client certificate.</span></span> <span data-ttu-id="b01e2-176">hello 개인 (My) 저장소에 로컬 컴퓨터 hello 또는 hello 현재 사용자의 hello 인증서를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-176">hello certificate can be installed into hello Personal (My) store of hello local computer or hello current user.</span></span>  <span data-ttu-id="b01e2-177">또한 해야 hello 서버 인증서의 지문 안녕하세요 hello 클라이언트 인증할 수 있도록 hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-177">You also need hello thumbprint of hello server certificate so that hello client can authenticate hello cluster.</span></span>

<span data-ttu-id="b01e2-178">다음 PowerShell cmdlet tooset hello 클러스터에 액세스할 수 있는 hello 컴퓨터에 클라이언트 인증서 hello hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-178">Run hello following PowerShell cmdlet tooset up hello client certificate on hello computer from which you access hello cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="b01e2-179">자체 서명 된 인증서 인 경우이 인증서 tooconnect tooa 보안 클러스터를 사용 하기 전에 저장 하는 것 tooyour 컴퓨터의 "신뢰할 수 있는 사용자" tooimport를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b01e2-179">If it is a self-signed certificate, you need tooimport it tooyour machine's "trusted people" store before you can use this certificate tooconnect tooa secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="b01e2-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b01e2-180">Next steps</span></span>

* [<span data-ttu-id="b01e2-181">서비스 패브릭 클러스터 업그레이드 프로세스 및 사용자 기대 수준</span><span class="sxs-lookup"><span data-stu-id="b01e2-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="b01e2-182">Visual Studio에서 서비스 패브릭 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="b01e2-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="b01e2-183">서비스 패브릭 상태 모델 소개</span><span class="sxs-lookup"><span data-stu-id="b01e2-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="b01e2-184">응용 프로그램 보안 및 RunAs</span><span class="sxs-lookup"><span data-stu-id="b01e2-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="b01e2-185">Service Fabric CLI 시작</span><span class="sxs-lookup"><span data-stu-id="b01e2-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
