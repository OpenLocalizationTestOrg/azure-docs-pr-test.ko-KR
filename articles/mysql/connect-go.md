---
title: "Go를 사용하여 MySQL용 Azure Database에 연결 | Microsoft Docs"
description: "이 빠른 시작에서는 MySQL용 Azure Database에서 데이터를 연결하고 쿼리하는 데 사용할 수 있는 몇 가지 Go 코드 샘플을 제공합니다."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: 42a6b1c37de08971674c8b38f1e13bfd657f8b03
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="cb2ce-103">MySQL용 Azure Database: Go 언어를 사용하여 데이터 연결 및 쿼리</span><span class="sxs-lookup"><span data-stu-id="cb2ce-103">Azure Database for MySQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="cb2ce-104">이 빠른 시작에서는 Windows, Ubuntu Linux 및 Apple macOS 플랫폼에서 [Go](https://golang.org/) 언어로 작성된 코드를 사용하여 MySQL용 Azure Database에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using code written in the [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="cb2ce-105">SQL 문을 사용하여 데이터베이스의 데이터를 쿼리, 삽입, 업데이트 및 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="cb2ce-106">이 문서에서는 Go를 사용하여 개발하는 데 익숙하고 MySQL용 Azure Database를 처음 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb2ce-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="cb2ce-107">Prerequisites</span></span>
<span data-ttu-id="cb2ce-108">이 빠른 시작에서는 다음과 같은 가이드 중 하나에서 만들어진 리소스를 시작 지점으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="cb2ce-109">Azure Portal을 사용한 MySQL용 Azure Database 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="cb2ce-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="cb2ce-110">Azure CLI를 사용한 MySQL용 Azure 데이터베이스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="cb2ce-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="cb2ce-111">Go 및 MySQL 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="cb2ce-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="cb2ce-112">[Go](https://golang.org/doc/install) 및 [MySQL용 go-sql-driver(영문)](https://github.com/go-sql-driver/mysql#installation)를 자신의 컴퓨터에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-112">Install [Go](https://golang.org/doc/install) and the [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="cb2ce-113">플랫폼에 따라 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="cb2ce-114">Windows</span><span class="sxs-lookup"><span data-stu-id="cb2ce-114">Windows</span></span>
1. <span data-ttu-id="cb2ce-115">[설치 지침](https://golang.org/doc/install)에 따라 Microsoft Windows용 Go를 [다운로드](https://golang.org/dl/)하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="cb2ce-116">[시작] 메뉴에서 [명령 프롬프트]를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="cb2ce-117">다음과 같이 프로젝트 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-117">Make a folder for your project such.</span></span> <span data-ttu-id="cb2ce-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="cb2ce-119">디렉터리를 프로젝트 폴더로 변경합니다(예: `cd %USERPROFILE%\go\src\mysqlgo`).</span><span class="sxs-lookup"><span data-stu-id="cb2ce-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="cb2ce-120">소스 코드 디렉터리를 가리키도록 GOPATH에 대한 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="cb2ce-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="cb2ce-122">`go get github.com/go-sql-driver/mysql` 명령을 실행하여 [MySQL용 go-sql-driver(영문)](https://github.com/go-sql-driver/mysql#installation)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-122">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="cb2ce-123">요약하자면, Go 설치 후 명령 프롬프트에서 다음이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="cb2ce-124">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="cb2ce-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="cb2ce-125">Bash 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="cb2ce-126">`sudo apt-get install golang-go`를 실행하여 Go를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="cb2ce-127">홈 디렉터리에서 프로젝트 폴더를 만듭니다(예: `mkdir -p ~/go/src/mysqlgo/`).</span><span class="sxs-lookup"><span data-stu-id="cb2ce-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="cb2ce-128">디렉터리를 폴더로 변경합니다(예: `cd ~/go/src/mysqlgo/`).</span><span class="sxs-lookup"><span data-stu-id="cb2ce-128">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="cb2ce-129">현재 홈 디렉터리의 go 폴더와 같이 유효한 소스 디렉터리를 가리키도록 GOPATH 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="cb2ce-130">Bash 셸에서 `export GOPATH=~/go`를 실행하여 go 디렉터리를 현재 셸 세션에 대한 GOPATH로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="cb2ce-131">`go get github.com/go-sql-driver/mysql` 명령을 실행하여 [MySQL용 go-sql-driver(영문)](https://github.com/go-sql-driver/mysql#installation)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-131">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="cb2ce-132">요약하자면, 다음과 같은 Bash 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="cb2ce-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="cb2ce-133">Apple macOS</span></span>
1. <span data-ttu-id="cb2ce-134">해당 플랫폼과 일치하는 [설치 지침](https://golang.org/doc/install)에 따라 Go를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="cb2ce-135">Bash 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="cb2ce-136">홈 디렉터리에서 프로젝트 폴더를 만듭니다(예: `mkdir -p ~/go/src/mysqlgo/`).</span><span class="sxs-lookup"><span data-stu-id="cb2ce-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="cb2ce-137">디렉터리를 폴더로 변경합니다(예: `cd ~/go/src/mysqlgo/`).</span><span class="sxs-lookup"><span data-stu-id="cb2ce-137">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="cb2ce-138">현재 홈 디렉터리의 go 폴더와 같이 유효한 소스 디렉터리를 가리키도록 GOPATH 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="cb2ce-139">Bash 셸에서 `export GOPATH=~/go`를 실행하여 go 디렉터리를 현재 셸 세션에 대한 GOPATH로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="cb2ce-140">`go get github.com/go-sql-driver/mysql` 명령을 실행하여 [MySQL용 go-sql-driver(영문)](https://github.com/go-sql-driver/mysql#installation)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-140">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="cb2ce-141">요약하자면, Go 설치 후 다음 bash 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="cb2ce-142">연결 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="cb2ce-142">Get connection information</span></span>
<span data-ttu-id="cb2ce-143">MySQL용 Azure Database에 연결하는 데 필요한 연결 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-143">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="cb2ce-144">정규화된 서버 이름 및 로그인 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="cb2ce-145">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cb2ce-146">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭하고 만든 서버를 검색합니다(예: **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="cb2ce-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="cb2ce-147">**myserver4demo** 서버 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-147">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="cb2ce-148">서버의 **속성** 페이지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-148">Select the server's **Properties** page.</span></span> <span data-ttu-id="cb2ce-149">**서버 이름** 및 **서버 관리자 로그인 이름**을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="cb2ce-150">![MySQL용 Azure Database - 서버 관리자 로그인](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="cb2ce-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="cb2ce-151">서버 로그인 정보를 잊어버린 경우 **개요** 페이지로 이동하여 서버 관리자 로그인 이름을 확인하고 필요한 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-151">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="cb2ce-152">Go 코드 작성 및 실행</span><span class="sxs-lookup"><span data-stu-id="cb2ce-152">Build and run Go code</span></span> 
1. <span data-ttu-id="cb2ce-153">Golang 코드를 작성하려면 Microsoft Windows의 메모장, Ubuntu의 [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) 또는 [Nano](https://www.nano-editor.org/), macOS의 TextEdit과 같은 간단한 텍스트 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-153">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="cb2ce-154">보다 풍부한 IDE(대화형 개발 환경)를 선호하는 경우 Jetbrains의 [Gogland](https://www.jetbrains.com/go/), Microsoft의 [Visual Studio Code](https://code.visualstudio.com/) 또는 [Atom](https://atom.io/)을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="cb2ce-155">아래 섹션에서 Go 코드를 텍스트 파일에 붙여넣고 `%USERPROFILE%\go\src\mysqlgo\createtable.go`(Windows 경로) 또는 `~/go/src/mysqlgo/createtable.go`(Linux 경로)와 같이 \*.go 파일 확장명이 포함된 프로젝트 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-155">Paste the Go code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="cb2ce-156">코드에서 `HOST`, `DATABASE`, `USER` 및 `PASSWORD` 상수를 찾아 예제 값을 사용자 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-156">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span> 
4. <span data-ttu-id="cb2ce-157">명령 프롬프트 또는 Bash 셸을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-157">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="cb2ce-158">디렉터리를 프로젝트 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-158">Change directory into your project folder.</span></span> <span data-ttu-id="cb2ce-159">예를 들어 Windows에서는 `cd %USERPROFILE%\go\src\mysqlgo\`이고,</span><span class="sxs-lookup"><span data-stu-id="cb2ce-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="cb2ce-160">Linux에서는 `cd ~/go/src/mysqlgo/`입니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="cb2ce-161">언급된 일부 IDE 편집기에서는 셸 명령 없이 디버그 및 런타임 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-161">Some of the IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="cb2ce-162">응용 프로그램을 컴파일하고 실행하려면 `go run createtable.go` 명령을 입력하여 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-162">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="cb2ce-163">또는 `go build createtable.go` 네이티브 응용 프로그램에 코드를 빌드하려면 `createtable.exe`를 시작하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-163">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="cb2ce-164">테이블 연결, 생성 및 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="cb2ce-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="cb2ce-165">다음 코드를 사용하여 서버에 연결하고, 테이블을 만들고, **INSERT** SQL 문을 통해 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-165">Use the following code to connect to the server, create a table, and load the data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="cb2ce-166">이 코드는 세 개의 패키지, 즉 [sql 패키지](https://golang.org/pkg/database/sql/), MySQL용 Azure Database와 통신할 드라이버로 사용되는 [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation), 명령줄에 출력되는 입출력을 위한 [fmt 패키지](https://golang.org/pkg/fmt/)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-166">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="cb2ce-167">[sql.Open()](http://go-database-sql.org/accessing.html) 메서드를 호출하여 MySQL용 Azure Database에 연결하고 [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) 메서드를 사용하여 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-167">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="cb2ce-168">[데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB)은 이러한 과정 내내 사용되며 데이터베이스 서버에 대한 연결 풀을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="cb2ce-169">[Exec()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드를 여러 번 호출하여 여러 DDL 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-169">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several DDL commands.</span></span> <span data-ttu-id="cb2ce-170">또한 [Prepare()](http://go-database-sql.org/prepared.html) 및 Exec()를 사용하여 다른 매개 변수로 준비된 문을 실행하여 3개 행을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-170">The code also uses the [Prepare()](http://go-database-sql.org/prepared.html) and Exec() to run prepared statements with different parameters to insert three rows.</span></span> <span data-ttu-id="cb2ce-171">매번 사용자 지정 checkError() 메서드를 사용하여, 오류가 발생하여 서둘러 종료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-171">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="cb2ce-172">`host`, `database`, `user` 및 `password` 상수는 원하는 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-172">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a><span data-ttu-id="cb2ce-173">데이터 읽기</span><span class="sxs-lookup"><span data-stu-id="cb2ce-173">Read data</span></span>
<span data-ttu-id="cb2ce-174">**SELECT** SQL 문을 사용하여 데이터를 연결하고 읽으려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="cb2ce-175">이 코드는 세 개의 패키지, 즉 [sql 패키지](https://golang.org/pkg/database/sql/), MySQL용 Azure Database와 통신할 드라이버로 사용되는 [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation), 명령줄에 출력되는 입출력을 위한 [fmt 패키지](https://golang.org/pkg/fmt/)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="cb2ce-176">[sql.Open()](http://go-database-sql.org/accessing.html) 메서드를 호출하여 MySQL용 Azure Database에 연결하고 [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) 메서드를 사용하여 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-176">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="cb2ce-177">[데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB)은 이러한 과정 내내 사용되며 데이터베이스 서버에 대한 연결 풀을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="cb2ce-178">[Query()](https://golang.org/pkg/database/sql/#DB.Query) 메서드를 호출하여 select 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-178">The code calls the [Query()](https://golang.org/pkg/database/sql/#DB.Query) method to run the select command.</span></span> <span data-ttu-id="cb2ce-179">그런 다음 [Next()](https://golang.org/pkg/database/sql/#Rows.Next)를 실행하여 결과 집합을 반복하고 [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan)을 사용하여 열 값을 구문 분석하여 변수에 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) to iterate through the result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) to parse the column values, saving the value into variables.</span></span> <span data-ttu-id="cb2ce-180">매번 사용자 지정 checkError() 메서드를 사용하여, 오류가 발생하여 서둘러 종료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-180">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="cb2ce-181">`host`, `database`, `user` 및 `password` 상수는 원하는 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-181">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from the table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a><span data-ttu-id="cb2ce-182">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="cb2ce-182">Update data</span></span>
<span data-ttu-id="cb2ce-183">**UPDATE** SQL 문을 사용하여 데이터를 연결하고 업데이트하려면 다음 코드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="cb2ce-184">이 코드는 세 개의 패키지, 즉 [sql 패키지](https://golang.org/pkg/database/sql/), MySQL용 Azure Database와 통신할 드라이버로 사용되는 [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation), 명령줄에 출력되는 입출력을 위한 [fmt 패키지](https://golang.org/pkg/fmt/)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="cb2ce-185">[sql.Open()](http://go-database-sql.org/accessing.html) 메서드를 호출하여 MySQL용 Azure Database에 연결하고 [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) 메서드를 사용하여 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-185">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="cb2ce-186">[데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB)은 이러한 과정 내내 사용되며 데이터베이스 서버에 대한 연결 풀을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="cb2ce-187">[Exec()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드를 호출하여 update 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the update command.</span></span> <span data-ttu-id="cb2ce-188">매번 사용자 지정 checkError() 메서드를 사용하여, 오류가 발생하여 서둘러 종료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-188">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="cb2ce-189">`host`, `database`, `user` 및 `password` 상수는 원하는 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-189">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a><span data-ttu-id="cb2ce-190">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="cb2ce-190">Delete data</span></span>
<span data-ttu-id="cb2ce-191">다음 코드를 사용하여 데이터를 연결하고 **DELETE** SQL 문을 통해 데이터를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-191">Use the following code to connect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="cb2ce-192">이 코드는 세 개의 패키지, 즉 [sql 패키지](https://golang.org/pkg/database/sql/), MySQL용 Azure Database와 통신할 드라이버로 사용되는 [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation), 명령줄에 출력되는 입출력을 위한 [fmt 패키지](https://golang.org/pkg/fmt/)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="cb2ce-193">[sql.Open()](http://go-database-sql.org/accessing.html) 메서드를 호출하여 MySQL용 Azure Database에 연결하고 [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) 메서드를 사용하여 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-193">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="cb2ce-194">[데이터베이스 핸들](https://golang.org/pkg/database/sql/#DB)은 이러한 과정 내내 사용되며 데이터베이스 서버에 대한 연결 풀을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="cb2ce-195">[Exec()](https://golang.org/pkg/database/sql/#DB.Exec) 메서드를 호출하여 delete 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the delete command.</span></span> <span data-ttu-id="cb2ce-196">매번 사용자 지정 checkError() 메서드를 사용하여, 오류가 발생하여 서둘러 종료했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-196">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="cb2ce-197">`host`, `database`, `user` 및 `password` 상수는 원하는 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cb2ce-197">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a><span data-ttu-id="cb2ce-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb2ce-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="cb2ce-199">내보내기 및 가져오기를 사용하여 데이터베이스 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="cb2ce-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
