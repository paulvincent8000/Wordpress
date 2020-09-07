# Safely embed an Email address

Use this javascript snippen to embed the address as a html block.
``` html
<p><em>This text tells you to send an email to  

<script language="JavaScript">

var username = "secretaris";
var hostname = "amervallei.nl";
var linktext = username + "@" + hostname ;

document.write("<a href='" + "mail" + "to:" + username + "@" + hostname + "'>" + linktext + "</a>");

</script>

and this text follows the email address.</em></p>
```
