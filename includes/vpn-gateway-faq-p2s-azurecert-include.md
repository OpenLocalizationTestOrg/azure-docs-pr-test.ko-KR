[!INCLUDE [P2S FAQ All](vpn-gateway-faq-p2s-all-include.md)]

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>지점 및 사이트 간 연결에 내부 PKI 루트 CA를 사용할 수 있습니까?

예. 이전에는 자체 서명한 루트 인증서만 사용할 수 있었습니다. 여전히 20개의 루트 인증서를 업로드할 수 있습니다.

### <a name="what-tools-can-i-use-to-create-certificates"></a>인증서를 만들려면 어떤 도구를 사용합니까?

You can use your Enterprise PKI 솔루션(사용자 인터넷 PKI), Azure PowerShell, MakeCert 및 OpenSSL을 사용할 수 있습니다.

### <a name="certsettings"></a>인증서 설정 및 매개 변수에 대한 지침이 있습니까?

* **Internal PKI/Enterprise PKI 솔루션:** [인증서 생성](../articles/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md#generatecert)단계를 봅니다.

* **Azure PowerShell:** 단계는 [Azure PowerShell](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md) 문서를 참조하세요.

* **Makecert:** 단계는 [Makecert](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md) 문서를 참조하세요.

* **OpenSSL:** 

    * 인증서를 내보낼 때는 루트 인증서를 Base64로 변환해야 합니다.

    * 클라이언트 인증서:

      * 개인 키를 만들 때에는 길이를 4096으로 지정합니다.
      * 인증서를 만들 때에는 *-extensions* 매개 변수에 대해 *usr_cert*를 지정합니다.