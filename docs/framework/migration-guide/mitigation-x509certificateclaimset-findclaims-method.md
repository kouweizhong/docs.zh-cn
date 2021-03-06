---
title: "缓解：X509CertificateClaimSet.FindClaims 方法 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ee356e3b-f932-48f5-875a-5e42340bee63
caps.latest.revision: 7
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: c234d6ddeda50dfefff8c49a2e14d623cdd8d861
ms.contentlocale: zh-cn
ms.lasthandoff: 04/18/2017

---
# <a name="mitigation-x509certificateclaimsetfindclaims-method"></a>缓解：X509CertificateClaimSet.FindClaims 方法
从面向 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 的应用开始，<xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=fullName> 方法会尝试使 `claimType` 自变量与其 SAN 字段中的所有 DNS 条目相匹配。  
  
## <a name="impact"></a>影响  
 此更改仅影响面向从 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 开始的 .NET Framework 版本的应用。  
  
 对于面向 .NET Framework 以前版本的应用，<xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=fullName> 方法会尝试使 `claimType` 自变量仅与最后一个 DNS 条目相匹配。  
  
## <a name="mitigation"></a>缓解  
 如果无需进行此更改，则面向从 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 开始的 .NET Framework 版本的应用可通过将以下配置设置添加到应用配置文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分，来选择放弃更改：  
  
```xml  
<runtime>  
   <AppContextSwitchOverrides value="Switch.System.IdentityModel.DisableMultipleDNSEntriesInSANCertificate=true" />   
</runtime>  
```  
  
 此外，面向 .NET Framework 以前版本但在 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] 或更高版本下运行的应用可通过将以下配置设置添加到应用配置文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分，来选择实现此行为：  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.IdentityModel.DisableMultipleDNSEntriesInSANCertificate=false" />   
</runtime>  
```  
  
## <a name="see-also"></a>另请参阅  
 [重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-1.md)

