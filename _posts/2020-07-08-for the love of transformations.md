---
layout: post
title: "For The Love Of Transformations"
---

XSLT, have been around for decades. It saw three release overtime, version 3 being the most recent, and with the availability of better functions. However, the lack of support for xslt 3.0 in major IDEs and code editors seems to be a hinderance in it’s wider acceptability, and so the xslt 1.0 remains the choice for transformation still.

I recently stumbled upon this need to loop over a fixed set of values using xslt 1.0, which was then to be used in an Azure integration account for transformations.

The first solution was to use the inbuilt document function, something like below

`
<!--let's say we want to loop over x, y and z-->
<xsl:variable name="var:valuesToLoopOver"> 
    <item>x</item>
    <item>y</item>
    <item>z</item>
</xsl:variable>

<xsl:variable name="var:values" select="document('')//xsl:variable[@name='var:valuesToLoopOver']/*">

<xsl:for-each select="$var:values">
    <data>
        <xsl:value-of select="." />
    </data>
</xsl:for-each>
`

Look good, works well from visual studio too, only problem is that Azure Integration Account does not likes it. It seems to have and issue with the document(‘’) function, and so the solution had to be built with a kind of recursive call to transformation sub-template.

`
<xsl:call-template name="valuesToLoopOver">
    <xsl:with-param name="values" select="'x,y,z,'" />
</xsl:call-template>

<xsl:template name="valuesToLoopOver">
    <xsl:param name="values" />    
    <xsl:if test="string-length($values) > 0">
        <xsl:variable name="var:value" select="substring-before($values,',')">
            <data>
                <xsl:value-of select="$var:value">
            </data>
            <xsl:call-template name="valuesToLoopOver">
                <xsl:with-param name="values" select="substring-after($var:values,',')" />
            </xsl:call-template>
    </xsl:if>
</xsl:template>
`