php-sms-from-webiste
====================

**Learn how to really exploit and implement an SMS solution to your website in PHP**

In the last 15 years the technology and the communication methods showed outstanding improvements. 
There is plenty of undiscovered opportunites in this sector. One of them is website implementation. 
The potencial in the SMS communication sector will increase in the next five years. 

It is faster, cheaper and more efficient than other marketing tool. The opening rate of SMS messages is 97%.  
There is no other marketing tool like the SMS marketing if you wish to reach your consumers. 
You can check every detail about your message in a delivery report and with good marketing 
you can engage consumers to your company.

You can use the SMS to send service alerts (send message to your registered customers about blackFriday, cyberMonday sales),
verifications (security codes for log-in), reminders (about the closing deadline for your colleauges, last minute promotions).
If you have a webshop, you can send receipts or if you are a retailer you can surprise your visiting consumers 
with an SMS what hides a coupon for a personalised daily sale not to mention about the graphic messages. 

Since we are living in the era of ”smart devices” every mobile user can open a link in a message or share a coupon 
with his/her friends.

If you can integrate this simplex communication form for your marketing plan 
even if you implement this solution to your website you can reach outstanding results. 

In this article, you can learn how to create an SMS solution in your website.

To integrate an SMS functionality to your website,all you have to do is to follow 4 easy and quick steps. 

•	Step 1 –Install Ozeki NG SMS Gateway to your computer. 

You can download and try the trial version for free in the following website: http://ozekisms.com/index.php?owpn=112

•	Step 2 – Create a HTML form for sending text messages.

To get this solution working you have to save the sendsms.html file to your webserver.

Here is the source to create the html file:
...

<html>
 <body>
   <h1>My SMS form</h1>
   <form method=post action='sendsms.php'>
   <table border=0>
   <tr>
     <td>Recipient</td>
     <td><input type='text' name='recipient'></td>
   </tr>
   <tr>
     <td>Message</td>
     <td><textarea rows=4 cols=40 name='message'></textarea></td>
   </tr>
   <tr>
     <td> </td>
     <td><input type=submit name=submit value=Send></td>
   </tr>
   </table>
   </form>
 </body>
</html>

...

•	Step 3 – Create your PHP SMS Script

The HTML form will send the data about your text message to your php script, which will forward this information to the SMS Gateway.

Here is the source code to create the php script:

...
########################################################
# Login information for the SMS Gateway
########################################################

$ozeki_user = "admin";
$ozeki_password = "abc123";
$ozeki_url = "http://127.0.0.1:9501/api?";

########################################################
# Functions used to send the SMS message
########################################################
function httpRequest($url){
    $pattern = "/http...([0-9a-zA-Z-.]*).([0-9]*).(.*)/";
    preg_match($pattern,$url,$args);
    $in = "";
    $fp = fsockopen("$args[1]", $args[2], $errno, $errstr, 30);
    if (!$fp) {
       return("$errstr ($errno)");
    } else {
        $out = "GET /$args[3] HTTP/1.1\r\n";
        $out .= "Host: $args[1]:$args[2]\r\n";
        $out .= "User-agent: Ozeki PHP client\r\n";
        $out .= "Accept: */*\r\n";
        $out .= "Connection: Close\r\n\r\n";

        fwrite($fp, $out);
        while (!feof($fp)) {
           $in.=fgets($fp, 128);
        }
    }
    fclose($fp);
    return($in);
}



function ozekiSend($phone, $msg, $debug=false){
      global $ozeki_user,$ozeki_password,$ozeki_url;

      $url = 'username='.$ozeki_user;
      $url.= '&password='.$ozeki_password;
      $url.= '&action=sendmessage';
      $url.= '&messagetype=SMS:TEXT';
      $url.= '&recipient='.urlencode($phone);
      $url.= '&messagedata='.urlencode($msg);

      $urltouse =  $ozeki_url.$url;
      if ($debug) { echo "Request: <br>$urltouse<br><br>"; }

      //Open the URL to send the message
      $response = httpRequest($urltouse);
      if ($debug) {
           echo "Response: <br><pre>".
           str_replace(array("<",">"),array("&lt;","&gt;"),$response).
           "</pre><br>"; }

      return($response);
}

########################################################
# GET data from sendsms.html
########################################################

$phonenum = $_POST['recipient'];
$message = $_POST['message'];
$debug = true;

ozekiSend($phonenum,$message,$debug);
...

(In order to be able to use this PHP script, you need to have the Ozeki NG SMS Gateway software 
installed on your computer. 
After Ozeki NG SMS Gateway is installed and configured, change the value of the $ozeki_url variable 
in the above PHP script to reflect the IP address of your computer.)

If you wish to start increasing your marketing ROI indicator or you just want to boost your website 
with an implemented solution search for more information about Ozeki SMS Gateway.
