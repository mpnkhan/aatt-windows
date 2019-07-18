# Automated Accessibility Testing Tool (AATT)

Browser-based accessibility testing tools and plugins require manually testing each page, one at a time. Tools that can crawl a website can only scan pages that do not require login credentials, and that are not behind a firewall. Instead of developing, testing, and using a separate accessibility test suite, you can now integrate accessibility testing into your existing automation test suite using AATT.
 

## Windows setup 

```sh
$ git clone https://github.com/paypal/AATT.git
$ cd AATT
$ npm i
$ DEBUG=AATT* http_port=3000 node app.js
```

You can now access the running instance of AATT from http://localhost:3000
To test the api do 
http://localhost:3000/test/AATT_API.html
and click submit

## Note
Though the UI may show testing URL and  html this is primarily intended to do continous integration with selenium suites using the API hosted internally in your environment


## Integration with AATT API
AATT provides an API for evaluating HTML Source code from other servers. The API EndPoint is: https://your_nodejs_server/evaluate

* Accepts the following parameters:
  1. "source" to send the HTML source of the page. Can be a whole page or partial page source 
  2. "engine" E.g. engine=htmlcs. This is the engine which will scan the code. It accepts a single value of "axe", chrome" or "htmlcs". 
  3. "ouput" to get the jsonified string. E.g. output=json.  If this parameter is not set or left empty, it will return a string with table data that can be parsed or appended directly into your page.
  Default to "htmlcs"
  4. "errLevel" Error level like Error, Warning or Notices .  Mapped to 1, 2 and 3 respectively. E.g. "1,2,3"
  5. "level" This option applies only for the default htmlcs evaluation engine. Options can be either of the following WCAG2AA, WCAG2A, WCAG2AAA, Section508  . Defaults to "WCAG2A"

    
* Set the Request Header Content-type as application/x-www-form-urlencoded

## Example
 
Here is a sample ajax script which would initiate the request:

``` html
var xmlhttp = new XMLHttpRequest();
xmlhttp.open("POST","http://your_nodejs_server/evaluate",true); 
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("source=" + document.getElementById('source').value;

```

## How to Use with nightwatchJS
[Nightwatch JS](http://nightwatchjs.org ) is another UI automated testing framework powered by Node.js and uses the Selenium WebDriver API. To call AATT, you need to use the [request module](https://github.com/request/request). NightwatchJs has call back functions like before and after hooks that would be called before or after executing a test case. Request to AATT API should be done in after hook passing the source code of the page to the API.  Here is an [example commit](https://github.com/mpnkhan/nightwatch/commit/a377e860e0bfbd21d9e365e86fb3e6c4ec0e63f0)  on how to do this with Nightwatch. 

## License
BSD license](LICENSE.md).

[1]: https://yourhostname/evaluate "AATT api"

## Contributors
 - Prem Nawaz Khan,  developer || [https://github.com/mpnkhan](https://github.com/mpnkhan) || [@mpnkhan](https://twitter.com/mpnkhan)
 - Srinivasu Chakravarthula, user interaction, testing || @csrinivasu

## Feedback
We welcome your feedback. Please file issues and/or enhancement requests.

