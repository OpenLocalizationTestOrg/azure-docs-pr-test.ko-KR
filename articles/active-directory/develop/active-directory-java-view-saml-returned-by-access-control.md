---
title: "액세스 제어 서비스(Java)에서 반환되는 SAML 보기"
description: "Azure에서 호스팅되는 Java 응용 프로그램에서 액세스 제어 서비스에서 반환되는 SAML을 확인하는 방법에 대해 알아봅니다."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: 1552e624a4703138ab82f7133ceaec3dbd04e1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-view-saml-returned-by-the-azure-access-control-service"></a><span data-ttu-id="da7b2-103">Azure 액세스 제어 서비스에서 반환한 SAML을 보는 방법</span><span class="sxs-lookup"><span data-stu-id="da7b2-103">How to view SAML returned by the Azure Access Control Service</span></span>
<span data-ttu-id="da7b2-104">이 가이드에서는 Azure ACS(액세스 제어 서비스)에서 응용 프로그램에 반환하는 기본 SAML(Security Assertion Markup Language)을 보는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-104">This guide will show you how to view the underlying Security Assertion Markup Language (SAML) returned to your application by the Azure Access Control Service (ACS).</span></span> <span data-ttu-id="da7b2-105">이 가이드는 [Eclipse를 사용하여 Azure 액세스 제어 서비스를 통해 웹 사용자를 인증하는 방법](active-directory-java-authenticate-users-access-control-eclipse.md) 항목의 내용을 바탕으로 하여 SAML 정보를 표시하는 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-105">The guide builds on the [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays the SAML information.</span></span> <span data-ttu-id="da7b2-106">완료된 응용 프로그램은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-106">The completed application will look similar to the following.</span></span>

![예제 SAML 출력][saml_output]

<span data-ttu-id="da7b2-108">ACS에 대한 자세한 내용은 [다음 단계](#next_steps) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da7b2-108">For more information on ACS, see the [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="da7b2-109">Azure Access Control Services Filter는 CTP(Community Technology Preview)입니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-109">The Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="da7b2-110">이 필터는 시험판 소프트웨어로서 Microsoft에서 공식적으로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="da7b2-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="da7b2-111">Prerequisites</span></span>
<span data-ttu-id="da7b2-112">이 가이드에서 작업을 완료하려면 [Eclipse를 사용하여 Azure 액세스 제어 서비스를 통해 웹 사용자를 인증하는 방법](active-directory-java-authenticate-users-access-control-eclipse.md) 에서 샘플을 완료하고 이 자습서를 시작할 때부터 이 샘플을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="da7b2-112">To complete the tasks in this guide, complete the sample at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as the starting point for this tutorial.</span></span>

## <a name="add-the-jspwriter-library-to-your-build-path-and-deployment-assembly"></a><span data-ttu-id="da7b2-113">빌드 경로 및 배포 어셈블리에 JspWriter 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="da7b2-113">Add the JspWriter library to your build path and deployment assembly</span></span>
<span data-ttu-id="da7b2-114">빌드 경로 및 배포 어셈블리에 **javax.servlet.jsp.JspWriter** 클래스를 포함하는 라이브러리를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-114">Add the library that contains the **javax.servlet.jsp.JspWriter** class to your build path and deployment assembly.</span></span> <span data-ttu-id="da7b2-115">Tomcat을 사용하는 경우 라이브러리는 Apache **lib** 폴더에 있는 **jsp-api.jar**입니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-115">If you are using Tomcat, the library is **jsp-api.jar**, which is located in the Apache **lib** folder.</span></span>

1. <span data-ttu-id="da7b2-116">Eclipse의 Project Explorer에서 **MyACSHelloWorld**를 마우스 오른쪽 단추로 클릭하고, **Build Path**, **Configure Build Path**, **Libraries** 탭을 차례로 클릭한 후 **Add External JARs**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click the **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="da7b2-117">**JAR Selection** 대화 상자에서 필요한 JAR로 이동하여 선택한 후 **Open**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-117">In the **JAR Selection** dialog, navigate to the necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="da7b2-118">**Properties for MyACSHelloWorld** 대화 상자가 열리면 **Deployment Assembly**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-118">With the **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="da7b2-119">**Web Deployment Assembly** 대화 상자에서 **Add**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-119">In the **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="da7b2-120">**New Assembly Directive** 대화 상자에서 **Java Build Path Entries**를 클릭한 후 **Next**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-120">In the **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="da7b2-121">적절한 라이브러리를 선택하고 **Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-121">Select the appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="da7b2-122">**OK**를 클릭하여 **Properties for MyACSHelloWorld** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-122">Click **OK** to close the **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-the-jsp-file-to-display-saml"></a><span data-ttu-id="da7b2-123">SAML을 표시하도록 JSP 파일 수정</span><span class="sxs-lookup"><span data-stu-id="da7b2-123">Modify the JSP file to display SAML</span></span>
<span data-ttu-id="da7b2-124">다음 코드를 사용하도록 **index.jsp** 를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-124">Modify **index.jsp** to use the following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print the text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out the child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate the names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish the sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process the child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate the child nodes of the doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-the-application"></a><span data-ttu-id="da7b2-125">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="da7b2-125">Run the application</span></span>
1. <span data-ttu-id="da7b2-126">[Eclipse를 사용하여 Azure 액세스 제어 서비스를 통해 웹 사용자를 인증하는 방법](active-directory-java-authenticate-users-access-control-eclipse.md)에 설명된 단계에 따라 응용 프로그램을 컴퓨터 에뮬레이터에서 실행하거나 Azure에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-126">Run your application in the computer emulator or deploy to Azure, using the steps documented at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="da7b2-127">브라우저를 실행하여 웹 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="da7b2-128">응용 프로그램에 로그온하면 ID 공급자에서 제공하는 보안 어설션을 비롯하여 SAML 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="da7b2-128">After you log on to your application, you'll see SAML information, including the security assertion provided by the identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da7b2-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da7b2-129">Next steps</span></span>
<span data-ttu-id="da7b2-130">ACS 기능을 자세히 살펴 보고 보다 정교한 시나리오를 실험하려면 [Access Control Service 2.0][Access Control Service 2.0]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da7b2-130">To further explore ACS's functionality and to experiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify the JSP file to display SAML]: #modify_jsp
[Add the JspWriter library to your build path and deployment assembly]: #add_library
[Run the application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How to Authenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
