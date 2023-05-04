Download Link: https://assignmentchef.com/product/solved-cse-4074-programming-assignment
<br>



<strong> </strong>

<strong>Socket Programming – HTTP Server and Proxy Server </strong>

In this project, you are required to implement a multi-threaded HTTP server that returns a document determined by the requested URI. You are also requested to implement a proxy server with some specific properties.

You are also required to use ApacheBench program for testing your servers.




<strong>1) Implementing a multithreaded web server  </strong>

You are required to implement an HTTP server that achieve the following requirements: <strong>a)</strong> Your server should be capable of providing concurrency via multi-threading.

<ol>

 <li>Your server program should take single argument which specifies the port number.</li>

 <li>Your server should return an HTML document according to the requested URI. The size of the document is determined by the requested URI (any size between 100 and 20,000 bytes). Your  server should remove the leading slash ‘/’ from the URI and extract the resulting string as an  integer (in decimal) that specify the size of the document to be sent to the client. For example,  if the request line is “GET /1500 HTTP/1.0”, your server should send back an HTML file  that contains exactly 1,500 bytes of text (When the client save the document on the local disk, the  file size should be 1,500 bytes). The returned HTML file should have a proper HTML format  with &lt;HTML&gt;, &lt;HEAD&gt; and &lt;BODY&gt; tags, but the content can be anything. If the  requested URI asks for a size less than 100, or for a size greater than 20,000, or if the URL is not an integer, your server should not return any document, but instead it should return a “Bad Request” message with error code 400. If the method in request message is not GET, server would return “Not Implemented” (501) for valid HTTP methods other than GET, or “Bad Request” (400) for invalid methods.</li>

</ol>




As an example, the following document is 100 bytes long:




&lt;HTML&gt;

&lt;HEAD&gt;

&lt;TITLE&gt;I am 100 bytes long&lt;/TITLE&gt;

&lt;/HEAD&gt;

&lt;BODY&gt; a a a a a a a a &lt;/BODY&gt;

&lt;/HTML&gt;




<ol>

 <li>Your server must send back an HTTP response line, a Content-Type header and a ContentLength header. None of these count towards the size of the document.</li>

 <li>Your server should send back an HTTP response line that indicates an error if the requested URI is not a number, or is less than 100, or is greater than 20,000.</li>

 <li>Your server should print out information about every message received and every message sent.</li>

 <li>Your server should work when connected via a web browser (such as Internet Explorer or Google Chrome). For example, if the server port number is 8080, <a href="http://localhost:8080/500">http://localhost:8080/500</a> would be a valid URL if the server runs in the same host..</li>

</ol>













<strong>2) Implementing a proxy server  </strong>

You are required to implement a proxy server that achieves the following requirements:

<ol>

 <li>Your proxy server will not be able to cache HTTP objects. It just relays the request to the Web server implemented in the first step and send back the result to the client (as shown in the figure below).</li>

</ol>




<ol start="8888">

 <li>Proxy Server should use port 8888. Any client should be able to send a GET message to the proxy server as described in 1-c. But the proxy server would not generate any file, it would just direct GET message to the Web server. The result received from the web server would then passed to the client.</li>

 <li>Your proxy server only directs the requests to your web server. It doesn’t direct any request to another web server.<strong> </strong></li>

 <li>In this project, proxy server has a restriction. If the requested file size is greater than 9,999 (in other words, if the URI is greater than 9,999) it would not pass the request to the web server. Rather it sends “Request-URI Too Long” message with error code 414.</li>

 <li>If the Web Server is not running currently, your proxy server would return a “Not Found” error message with status code 404.</li>

 <li>The proxy server should work when connected via a browser after configuring the proxy settings of your browser. (Please check how to configure your web browser to use proxy. For example, in Internet Explorer, you can set the proxy in Tools &gt; Internet Options &gt; Connections Tab &gt; LAN Settings). Enter IP address of your web server for the proxy address (127.0.0.1 for localhost) and 8888 for the port.</li>

</ol>




When you configure proxy settings, all requests would be first directed to the proxy server. Your proxy server will accept a valid GET message from the client and forward it to the web server as follows:




Accept from client:

GET http://localhost:8080/500 HTTP/1.0




Send to web server:

GET /500 HTTP/1.0

Host: localhost:8080

(Additional client specified headers, if any…)







<table width="614">

 <tbody>

  <tr>

   <td width="614">$ ab -n 100 -c 10 mimoza.marmara.edu.tr/~omer.korcakThis is ApacheBench, Version 2.3 &lt;$Revision: 1843412 $&gt;Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/ Licensed to The Apache Software Foundation, http://www.apache.org/Benchmarking mimoza.marmara.edu.tr (be patient)…..doneServer Software:        ApacheServer Hostname:        mimoza.marmara.edu.trServer Port:            80 Document Path:          /~omer.korcakDocument Length:        250 bytes Concurrency Level:      10Time taken for tests:   2.905 secondsComplete requests:      100 Failed requests:        0Non-2xx responses:      100Total transferred:      49900 bytesHTML transferred:       25000 bytesRequests per second:    34.42 [#/sec] (mean)Time per request:       290.539 [ms] (mean)Time per request:       29.054 [ms] (mean, across all concurrent requests)Transfer rate:          16.77 [Kbytes/sec] receivedConnection Times (ms)min  mean[+/-sd] median   max Connect:       16   28   7.1     31      42Processing:    45  242  45.1    254     285Waiting:       31  174  61.6    180     277Total:         71  271  45.4    285     316Percentage of the requests served within a certain time (ms)   50%    28566%    28575%    28780%    29090%    30195%    30198%    30699%    316100%    316 (longest request)</td>

  </tr>

 </tbody>

</table>




You are required to download and run ab in your own PCs. You can use ab in either Windows or Linux (if you have any trouble to download and run ab, please contact to instructor). You can get detailed usage information by typing ‘ab –h’.

Using ab program, send 10 requests to http://ipv4.download.thinkbroadband.com/5MB.zip using following parameters:

<ol>

 <li>Send single request at a time (concurrency level = 1)</li>

</ol>

(use “ab –n 10 –c 1 http://ipv4.download.thinkbroadband.com/5MB.zip”).

<ol>

 <li>Send 5 requests at a time (concurrency level = 5).</li>

 <li>Send 10 requests at a time (concurrency level = 10).</li>

 <li>Repeat a), b) and c) using –k argument. This argument will send a “Connection: KeepAlive” header to the web server.</li>

</ol>




For each of the above cases, give the following obtained outputs. (It would be preferable to repeat the above tests several times and get the average).

<ol>

 <li>i) Time taken for tests (seconds) ii) Total transferred (bytes) and HTML transferred (bytes) iii) Time per request (ms) iv) Requests per second (#/sec) v) Transfer rate (Kbytes/sec)</li>

 <li>vi) Connection times</li>

</ol>




Clearly describe how and why these values change when you change concurrency level and when you use -k argument.




<ul>

 <li><strong>Testing your server using ApacheBench </strong></li>

</ul>

Use ApacheBench for debugging and testing your web server. “HTML transferred” should fit the requested document size. Moreover, perform a <strong>stress test</strong> for testing the performance of your server, as follows. Starting from one, increase number of parallel requests one by one and obtain the “time per request” and “requests per second” values. How do these values change by increasing level of concurrency? Maximum of how many concurrent requests do your server handle in a reasonable time? Comment on the results.

Repeat same tests for the proxy server. Comment on the results.





