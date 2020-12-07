---
title: 内部部署代理
ms.author: rusamai
author: rsamai
manager: jameslau
ms.audience: Admin
ms.topic: article
ms.service: mssearch
localization_priority: Normal
search.appverid:
- BFB160
- MET150
- MOE150
ROBOTS: NoIndex
description: 本地代理
ms.openlocfilehash: 763904f8dd96c5db8b0633e36795443502afe7d0
ms.sourcegitcommit: 0ed8ec8b3c4e0f5f669005081fd8b2219f07b4f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "49420830"
---
# <a name="graph-connector-agent"></a>图形连接器代理

若要使用本地图形连接器，需要安装 *graph 连接器代理* 软件。 它允许在本地数据和图形连接器 Api 之间进行安全的数据传输。 本文将指导您完成安装和配置代理。

## <a name="installation"></a>安装

[在此处](https://aka.ms/gcadownload)下载最新版本的 Graph 连接器代理，并使用安装向导安装该软件。 使用以下所述的计算机的推荐配置，软件最长可处理三个连接。 超过此数目的任何连接可能会降低代理上所有连接的性能。

建议的配置：

* Windows 10、Windows Server 2016 R2 及更高版本
* 8核，3 GHz
* 16 GB RAM，2 GB 磁盘空间
* 通过443对数据源和 internet 的网络访问

## <a name="create-and-configure-an-app-for-the-agent"></a>创建和配置代理的应用程序  

在使用代理之前，必须创建一个应用并配置身份验证详细信息。

### <a name="create-an-app"></a>创建应用程序

1. 转到 [Azure 门户](https://portal.azure.com) ，并使用管理员凭据登录租户。
2. 从导航窗格导航到 " **Azure Active Directory**  ->  **应用程序注册**"，然后选择 "**新建注册**"。
3. 提供应用程序的名称并选择 " **注册**"。
4. 记下应用程序 (客户端) ID。
5. 从导航窗格中打开 **API 权限** ，并选择 " **添加权限**"。
6. 依次选择 " **Microsoft Graph** " 和 " **应用程序权限**"。
7. 从权限中搜索 "ExternalItem" 和 "Directory. All" 并选择 " **添加权限**"。
8. 选择 " **授予管理员同意 [TenantName]** " 并通过选择 **"是"** 进行确认。
9. 检查权限是否处于 "已授予" 状态。
     ![权限显示为 "在右侧绿色中授予" 列。](media/onprem-agent/granted-state.png)

### <a name="configure-authentication"></a>配置身份验证

可以使用客户端密码或证书提供身份验证详细信息。 按照您选择的步骤进行操作。

#### <a name="configuring-the-client-secret-for-authentication"></a>配置客户端机密以进行身份验证

1. 转到 [Azure 门户](https://portal.azure.com) ，并使用管理员凭据登录租户。
2. 从导航窗格中打开 " **应用注册** "，然后转到相应的应用程序。 在 " **管理**" 下，选择 " **证书和密码**"。
3. 选择 " **新建客户端密码** "，然后选择密码的有效期。 复制生成的机密并将其保存，因为它不会再次显示。
4. 使用此客户端密码和应用程序 ID 配置代理。 不能在代理的 " **名称** " 字段中使用空格。 接受字母数字字符。

#### <a name="using-a-certificate-for-authentication"></a>使用证书进行身份验证

使用基于证书的身份验证有三个简单的步骤：

1. 创建或获取证书
1. 将证书上传到 Azure 门户
1. 将证书分配给代理

##### <a name="step-1-get-a-certificate"></a>步骤1：获取证书

下面的脚本可用于生成自签名证书。 您的组织可能不允许自签名证书。 在这种情况下，请使用此信息来了解这些要求，并根据组织的策略获取证书。

```Powershell
$dnsName = "<TenantDomain like agent.onmicrosoft.com>" # Your DNS name
$password = "<password>" # Certificate password
$folderPath = "D:\New folder\" # Where do you want the files to get saved to? The folder needs to exist.
$fileName = "agentcert" # What do you want to call the cert files? without the file extension
$yearsValid = 10 # Number of years until you need to renew the certificate
$certStoreLocation = "cert:\LocalMachine\My"
$expirationDate = (Get-Date).AddYears($yearsValid)
$certificate = New-SelfSignedCertificate -DnsName $dnsName -CertStoreLocation $certStoreLocation -NotAfter $expirationDate -KeyExportPolicy Exportable -KeySpec Signature
$certificatePath = $certStoreLocation + '\' + $certificate.Thumbprint
$filePath = $folderPath + '\' + $fileName
$securePassword = ConvertTo-SecureString -String $password -Force -AsPlainText
Export-Certificate -Cert $certificatePath -FilePath ($filePath + '.cer')
Export-PfxCertificate -Cert $certificatePath -FilePath ($filePath + '.pfx') -Password $securePassword
```

##### <a name="step-2-upload-the-certificate-in-the-azure-portal"></a>步骤2：在 Azure 门户中上传证书

1. 打开应用程序并导航到左侧窗格中的 "证书和密码" 部分
1. 选择 "上载证书" 并上载 .cer 文件
1. 打开 " **应用注册** "，然后从导航窗格中选择 " **证书和密码** "。 复制证书指纹。

![在左窗格中选择了 "证书和密码" 时的 thumbrint 证书列表](media/onprem-agent/certificates.png)

##### <a name="step-3-assign-the-certificate-to-the-agent"></a>步骤3：将证书分配给代理

如果使用了示例脚本生成证书，则可以在脚本中标识的位置找到 PFX 文件。

1. 将证书 pfx 文件下载到代理计算机上。
1. 双击 pfx 文件以启动 "证书安装" 对话框。
1. 安装证书时，为存储位置选择 "本地计算机"。
1. 安装证书后，通过 "开始" 菜单打开 "管理计算机证书"
1. 选择 "个人" 下新安装的证书-> "证书"
1. 右键单击证书，然后选择 "所有任务"-> "管理私钥 ..." 选项
1. 在 "权限" 对话框中，选择 "添加选项"。 在 "用户选择" 对话框中，写入： "NT Service\GcaHostService"，然后单击 "确定"。 不要单击 "检查姓名" 按钮。
1. 在 "权限" 对话框中单击 "确定"。 此时，代理计算机已配置为使用证书生成令牌的代理。