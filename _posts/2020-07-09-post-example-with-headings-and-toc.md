---
layout: post
title: "Namespaces, really ?"
---

Namespaces, are an integral part of BizTalk schemas definition. We need them because that’s how BizTalk generates strongly typed messages (concatenation of namespace and root node of the XSD) and then later identifies them. However, it’s definitely not a mandatory thing for Azure Integration Account. Schemas in Azure Account are perfectly fine, even without namespaces and this lessen the possible complications with XSLT mapping.

Argument is to get rid of namespaces, whenever possible and feasible. If you are using BizTalk server to define your schemas, for usages in Azure Integration Account, you can achieve this by setting the target namespace to empty string under properties window. This definitely makes the life a lot easier during the XSLT mapping. But then again, it’s not always possible to get rid of namespaces from the XMLs and consequently XSLT suffers.

There are two easy ways to handle the namespaces.

#### String Replace

The most easy way is to just use the string replace method on the input XML before sending it for transformation. I admit - it’s not the most elegant solution out there, but if it works, it ain't stupid !

#### Handle Namespaces in XSLT

You can also handle namespaces in XSLT, but defining the prefix and then using it in the XPATH expressions. Something like below snippet, where the messages would have contained namespace under prefix ns2

```
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"
                xmlns:ns2="http://www.blog.esrmnt.dev/xml/ns/posts/1.0"
                xmlns:var="http://schemas.microsoft.com/BizTalk/2003/var"
                xmlns:userCSharp="http://schemas.microsoft.com/BizTalk/2003/userCSharp"
                version="1.0">
<xsl:output omit-xml-decleration="no" method="xml" version="1.0" />

<xsl:template match="/">
    <post>
        <xsl:apply-templates select="/ns2:posts/ns2:post">
    </post>
</xsl:template>

<xsl:template match="ns2:post">

 <!--The rest of the mapping goes here-->

</xsl:template>
```