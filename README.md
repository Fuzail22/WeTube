<h1 align="center"> WeTube</h1>
<p align="center"> A video sharing platform where individuals can upload their video along with subtitles on specific timestamps and can view the videos on the platform with subtitles.</p>

## Deploying Backend
1. Create Amazon EC2 instnace Ubuntu ( ;-) ofcourse free tire ).
   >Download the .pem key during the process.
2. Using Putty gen convert the key.
   >For connecting with putty in windows we need the key to be in ppk form.
   >Refer [this](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html) link for detailed proceduring of connecting
   >with putty.
3. Connect with the ec2 instance using putty.
   > Default user name is <strong>ubuntu</strong>
4. Use [WinSCP](https://winscp.net/eng/index.php) to transfer our files to our remote ec2 instance.
   > In WinSCP the login can be done using the saved configuration from Putty.
   > Transfering files is simple drag and drop
5. After trasnfering files install python3.10
   ```
   sudo apt update
   ```
   ```
   sudo apt-get install python3.10
   ```
   > to check installation ```python3 --version```
6. Now we need to install a virtual environment to keep our packaga installations local to a specific env instead of global.
   ```
   
   
### Status Codes
1. 304 - The "304 Not Modified" status code is returned when the client (usually a web browser) makes a request for a resource that the server considers to be unchanged since the last time it was requested. The server then sends a response indicating that the client's cached version of the resource is still valid and can be used.
This behavior is due to the client sending an If-Modified-Since header in its request, indicating the timestamp of the version it currently has cached. If the server determines that the resource hasn't been modified since that timestamp, it returns a "304 Not Modified" response instead of the actual content, saving both bandwidth and processing time.
