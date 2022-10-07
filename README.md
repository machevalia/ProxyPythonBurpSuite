# ProxyPythonBurpSuite
How to proxy a python script through Burp Suite


1. Download the certificate from Burp Suite url
* Open your web browser and go to http://burpsuite.
* Click on “CA Certificate” button on the top right corner and save the certificate locally.
![image](https://user-images.githubusercontent.com/36945847/152576472-5bc54884-23b7-4756-a11a-3159f6028937.png)

2. Convert the certificate to PEM encoded format
* The certificate downloaded is DER formated and needs to be PEM encoded.
* You need to run the following command:
`openssl x509 -inform der -in cacert.der -out certificate.pem`
![image](https://user-images.githubusercontent.com/36945847/152576493-3d8ce1d5-0e98-441a-b405-4f33797ba37d.png)

3. Edit your python code
* Edit your python code with the following lines just below the import of Requests and OS modules:
```
import os

proxy = 'http://127.0.0.1:8080'
os.environ['http_proxy'] = proxy
os.environ['HTTP_PROXY'] = proxy
os.environ['https_proxy'] = proxy
os.environ['HTTPS_PROXY'] = proxy
os.environ['REQUESTS_CA_BUNDLE'] = "/path/to/cert/certificate.pem"
```
![image](https://user-images.githubusercontent.com/36945847/152576577-1a635d4f-71d6-403f-bb4b-a0e3084fc922.png)

4. Save and run!
