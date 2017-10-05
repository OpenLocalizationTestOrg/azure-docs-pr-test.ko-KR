---
title: "PostgreSQL용 Azure 데이터베이스에서 SSL 연결 구성 | Microsoft Docs"
description: "SSL 연결을 올바르게 사용하기 위해 PostgreSQL용 Azure 데이터베이스 및 연결된 응용 프로그램을 구성하는 방법에 대한 지침 및 정보"
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 685aa4c2f75b7c3260ca737f7c786157480b2d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="8e13c-103">PostgreSQL용 Azure 데이터베이스에서 SSL 연결 구성</span><span class="sxs-lookup"><span data-stu-id="8e13c-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="8e13c-104">PostgreSQL용 Azure 데이터베이스는 SSL(Secure Sockets Layer)을 사용해서 PostgreSQL 서비스에 클라이언트 응용 프로그램을 연결하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-104">Azure Database for PostgreSQL prefers connecting your client applications to the PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="8e13c-105">데이터베이스 서버와 클라이언트 응용 프로그램 간 SSL 연결을 적용하면 서버와 응용 프로그램 간 데이터 스트림을 암호화함으로써 “메시지 가로채기(man in the middle)” 공격으로부터 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

<span data-ttu-id="8e13c-106">기본적으로 PostgreSQL 데이터베이스 서비스는 SSL 연결을 요구하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-106">By default, the PostgreSQL database service is configured to require SSL connection.</span></span> <span data-ttu-id="8e13c-107">필요에 따라 클라이언트 응용 프로그램이 SSL 연결을 지원하지 않을 경우 데이터베이스 서비스에 연결하기 위해 SSL을 요구하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-107">Optionally, you can disable requiring SSL for connecting to your database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="8e13c-108">SSL 연결 적용</span><span class="sxs-lookup"><span data-stu-id="8e13c-108">Enforcing SSL connections</span></span>
<span data-ttu-id="8e13c-109">Azure Portal 및 CLI를 통해 프로비전된 모든 MySQL용 Azure 데이터베이스 서버의 경우 SSL 연결 적용이 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-109">For all Azure Database for PostgreSQL servers provisioned through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="8e13c-110">마찬가지로, Azure Portal의 해당 서버에 있는 “연결 문자열” 설정에서 미리 정의된 연결 문자열에는 SSL을 사용하여 데이터베이스 서버에 연결하기 위한 일반적인 언어에 대한 필수 매개 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="8e13c-111">SSL 매개 변수는 “ssl=true” 또는 “sslmode=require” 또는 “sslmode=required” 및 다른 변형과 같은 커넥터에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="8e13c-112">SSL 적용 구성</span><span class="sxs-lookup"><span data-stu-id="8e13c-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="8e13c-113">필요에 따라 SSL 연결 적용을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="8e13c-114">Microsoft Azure는 항상 향상된 보안을 위해 **SSL 연결 적용** 설정을 사용하는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-114">Microsoft Azure recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="8e13c-115">Azure 포털 사용</span><span class="sxs-lookup"><span data-stu-id="8e13c-115">Using the Azure portal</span></span>
<span data-ttu-id="8e13c-116">PostgreSQL용 Azure 데이터베이스 서버를 방문하여 **연결 보안**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="8e13c-117">설정/해제 단추를 사용하여 **SSL 연결 적용** 설정을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-117">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="8e13c-118">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-118">Then click **Save**.</span></span> 

![연결 보안 - SSL 적용 사용 안 함](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="8e13c-120">**SSL 적용 상태** 표시기를 확인할 수 있는 **개요** 페이지에서 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-120">You can confirm the setting by viewing the **Overview** page to see the **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="8e13c-121">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="8e13c-121">Using Azure CLI</span></span>
<span data-ttu-id="8e13c-122">Azure CLI에서 `Enabled` 또는 `Disabled` 값을 각각 사용하여 **ssl-enforcement** 매개 변수를 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-122">You can enable or disable the **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="8e13c-123">응용 프로그램 또는 프레임워크가 SSL 연결을 지원하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="8e13c-124">Drupal 및 Django와 같은 데이터베이스 서비스용 PostgreSQL을 사용하는 많은 일반적인 응용 프로그램 프레임워크는 기본적으로 설치하는 동안 SSL을 사용하도록 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="8e13c-125">SSL 연결의 사용 설정은 설치 후 또는 응용 프로그램 특정 CLI 명령을 통해 수행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-125">Enabling SSL connectivity must be done after installation or through CLI commands specific to the application.</span></span> <span data-ttu-id="8e13c-126">PostgreSQL 서버에 SSL 연결이 적용되어 있고 연결된 응용 프로그램이 올바르게 구성되어 있지 않은 경우 응용 프로그램이 데이터베이스 서버에 연결하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-126">If your PostgreSQL server is enforcing SSL connections and the associated application is not configured properly, the application may fail to connect to your database server.</span></span> <span data-ttu-id="8e13c-127">응용 프로그램의 설명서를 참조하여 SSL 연결을 설정하는 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8e13c-127">Consult your application's documentation to learn how to enable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="8e13c-128">SSL 연결을 위해 인증서 확인이 필요한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8e13c-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="8e13c-129">경우에 따라 안전한 연결을 위해 응용 프로그램에 신뢰할 수 있는 CA(인증 기관) 인증서 파일(.cer)에서 생성되는 로컬 인증서 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) to connect securely.</span></span> <span data-ttu-id="8e13c-130">다음 단계를 참조하여 .cer 파일을 얻고, 인증서를 디코딩한 후 응용 프로그램에 바인딩하세요.</span><span class="sxs-lookup"><span data-stu-id="8e13c-130">See the following steps to obtain the .cer file, decode the certificate and bind it to your application.</span></span>

### <a name="download-the-certificate-file-from-the-certificate-authority-ca"></a><span data-ttu-id="8e13c-131">CA(인증 기관)에서 인증서 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="8e13c-131">Download the certificate file from the Certificate Authority (CA)</span></span> 
<span data-ttu-id="8e13c-132">PostgreSQL용 Azure 데이터베이스 서버와 함께 SSL을 통해 통신하는 데 필요한 인증서는 [여기](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-132">The certificate needed to communicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="8e13c-133">인증서 파일을 로컬로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-133">Download the certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="8e13c-134">컴퓨터에 OpenSSL 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="8e13c-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="8e13c-135">응용 프로그램을 데이터베이스 서버에 안전하게 연결하기 위해 필요한 인증서 파일을 디코딩하려면 OpenSSL을 로컬 컴퓨터에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-135">To decode the certificate file needed for your application to connect securely to your database server, you need to install OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="8e13c-136">Linux, OS X 또는 Unix</span><span class="sxs-lookup"><span data-stu-id="8e13c-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="8e13c-137">OpenSSL 라이브러리는 [OpenSSL Software Foundation](http://www.openssl.org)에서 직접 소스 코드로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-137">The OpenSSL libraries are provided in source code directly from the [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="8e13c-138">다음 지침에서는 Linux PC에 OpenSSL을 설치하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-138">The following instructions guide you through the steps necessary to install OpenSSL on your Linux PC.</span></span> <span data-ttu-id="8e13c-139">이 문서에서는 Ubuntu 12.04 이상에서 작동하는 것으로 알려진 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-139">This article uses commands known to work on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="8e13c-140">터미널 세션을 열고 OpenSSL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="8e13c-141">다운로드 패키지에서 파일 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-141">Extract the files from the download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="8e13c-142">파일 압축을 푼 디렉터리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-142">Enter the directory where the files were extracted.</span></span> <span data-ttu-id="8e13c-143">기본적으로 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="8e13c-144">다음 명령을 실행하여 OpenSSL을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-144">Configure OpenSSL by executing the following command.</span></span> <span data-ttu-id="8e13c-145">/usr/local/openssl과 다른 폴더의 파일을 원하면 다음을 적절하게 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-145">If you want the files in a folder different than /usr/local/openssl, make sure to change the following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="8e13c-146">이제 OpenSSL이 올바르게 구성되었으므로 인증서를 변환하기 위해 컴파일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-146">Now that OpenSSL is configured properly, you need to compile it to convert your certificate.</span></span> <span data-ttu-id="8e13c-147">컴파일하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-147">To compile, run the following command:</span></span>

```bash
make
```
<span data-ttu-id="8e13c-148">컴파일이 완료되면 다음 명령을 실행하여 OpenSSL을 실행 가능하도록 설치할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-148">Once compiling is complete, you're ready to install OpenSSL as an executable by running the following command:</span></span>
```bash
make install
```
<span data-ttu-id="8e13c-149">시스템에 OpenSSL이 성공적으로 설치되었는지 확인하려면 다음 명령을 실행하여 동일한 출력이 나타나는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-149">To confirm that you've successfully installed OpenSSL on your system, run the following command and check to make sure you get the same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="8e13c-150">성공적이라면 다음과 같은 메시지가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-150">If successful you should see the following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="8e13c-151">Windows의 경우</span><span class="sxs-lookup"><span data-stu-id="8e13c-151">For Windows</span></span>
<span data-ttu-id="8e13c-152">다음 방법을 수행하면 Windows PC에서 OpenSSL을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-152">Installing OpenSSL on a Windows PC can be done in the following ways:</span></span>
1. <span data-ttu-id="8e13c-153">**(권장)** Window 10 이상에서 기본 제공되는 Windows용 Bash 기능을 사용하면 OpenSSL이 기본적으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-153">**(Recommended)** Using the built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="8e13c-154">Windows 10의 Windows용 Bash 기능을 사용하도록 설정하는 방법에 대한 지침은 [여기](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-154">Instructions on how to enable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="8e13c-155">커뮤니티에서 제공되는 Win32/64 응용 프로그램을 다운로드하여,</span><span class="sxs-lookup"><span data-stu-id="8e13c-155">Through downloading a Win32/64 application provided by the community.</span></span> <span data-ttu-id="8e13c-156">OpenSSL Software Foundation에서 특정 Windows 설치 관리자를 제공하거나 보증하지는 않지만 사용 가능한 설치 관리자의 목록은 [여기](https://wiki.openssl.org/index.php/Binaries)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-156">While the OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="8e13c-157">인증서 파일 디코딩</span><span class="sxs-lookup"><span data-stu-id="8e13c-157">Decode your certificate file</span></span>
<span data-ttu-id="8e13c-158">다운로드한 루트 CA 파일은 암호화된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-158">The downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="8e13c-159">OpenSSL을 사용하여 인증서 파일을 디코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-159">Use OpenSSL to decode the certificate file.</span></span> <span data-ttu-id="8e13c-160">이렇게 하려면 다음 OpenSSL 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-160">To do so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-to-azure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="8e13c-161">SSL 인증서 인증을 사용하여 PostgreSQL용 Azure 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="8e13c-161">Connecting to Azure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="8e13c-162">이제 인증서를 성공적으로 디코딩했으므로 SSL을 통해 데이터베이스 서버에 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-162">Now that you have successfully decoded your certificate, you can now connect to your database server securely over SSL.</span></span> <span data-ttu-id="8e13c-163">서버 인증서 확인을 허용하려면 사용자의 홈 디렉터리에 있는 파일 ~/.postgresql/root.crt에 인증서를 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-163">To allow server certificate verification, the certificate must be placed in the file ~/.postgresql/root.crt in the user's home directory.</span></span> <span data-ttu-id="8e13c-164">(Microsoft Windows에서 이 파일의 이름은 %APPDATA%\postgresql\root.crt입니다.)</span><span class="sxs-lookup"><span data-stu-id="8e13c-164">(On Microsoft Windows the file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="8e13c-165">다음은 PostgreSQL용 Azure 데이터베이스에 연결하기 위한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-165">The following provides instructions for connecting to Azure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="8e13c-166">현재 서비스에 연결된 상태에서 "sslmode=verify-full"을 사용하는 경우 연결이 다음과 같은 오류로 실패하는 알려진 문제가 있습니다. _“&lt;region&gt;.control.database.windows.net”에 대한 서버 인증서(및 7개 다른 이름)가 호스트 이름 “&lt;servername&gt;.postgres.database.azure.com”과 일치하지 않습니다._</span><span class="sxs-lookup"><span data-stu-id="8e13c-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection to the service, the connection will fail with the following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="8e13c-167">"sslmode=verify-full"이 필요한 경우 서버 명명 규칙 **&lt;servername&gt;.database.windows.net**을 연결 문자열 호스트 이름으로 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="8e13c-167">If "sslmode=verify-full" is required, please use the server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="8e13c-168">나중에 이 제한을 제거할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-168">We plan to remove this limitation in the future.</span></span> <span data-ttu-id="8e13c-169">다른 [SSL 모드](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS)를 사용하여 연결하면 기본 호스트 명명 규칙 **&lt;servername&gt;.postgres.database.azure.com**을 계속 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue to use the preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="8e13c-170">psql 명령줄 유틸리티 사용</span><span class="sxs-lookup"><span data-stu-id="8e13c-170">Using psql command-line utility</span></span>
<span data-ttu-id="8e13c-171">다음 예제에서는 psql 명령줄 유틸리티를 사용하여 PostgreSQL 서버에 성공적으로 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-171">The following example shows you how to successfully connect to your PostgreSQL server using the psql command-line utility.</span></span> <span data-ttu-id="8e13c-172">만든 `root.crt` 파일과 `sslmode=verify-ca` 또는 `sslmode=verify-full` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-172">Use the `root.crt` file created and the `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="8e13c-173">PostgreSQL 명령줄 인터페이스를 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-173">Using the PostgreSQL command-line interface, execute the following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="8e13c-174">성공하면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-174">If successful, you receive the following output:</span></span>
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="8e13c-175">pgAdmin GUI 도구 사용</span><span class="sxs-lookup"><span data-stu-id="8e13c-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="8e13c-176">SSL을 통해 안전하게 연결하도록 pgAdmin 4를 구성하려면 `SSL mode = Verify-CA` 또는 `SSL mode = Verify-Full`을 다음과 같이 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e13c-176">Configuring pgAdmin 4 to connect securely over SSL requires you to set the `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![pgAdmin - 연결 - SSL 모드 Require 스크린샷](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="8e13c-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e13c-178">Next steps</span></span>
<span data-ttu-id="8e13c-179">[용 Azure 데이터베이스를 위한 연결 라이브러리](concepts-connection-libraries.md) 후에 다양한 응용 프로그램 연결 옵션 검토</span><span class="sxs-lookup"><span data-stu-id="8e13c-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
