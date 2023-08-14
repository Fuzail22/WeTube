<h1 align="center"> WeTube</h1>
<p align="center"> A video sharing platform where individuals can upload their video along with subtitles on specific timestamps and can view the videos on the platform with subtitles.</p>


### Prototype Video
* Want to watch how it works?
   * Click [here](https://www.loom.com/share/90fb46efbe9f4aa3b712200164f075aa?sid=cf86ee39-f933-4078-8f05-af9c790e9dd4)
   * ![Frontend](FrontendSmall.png)
## Deploying Backend
1. Create Amazon EC2 instnace Ubuntu (ofcourse free tire 😉).
   >Download the .pem key during the process.
2. Using Putty gen convert the key.
   >For connecting with putty in windows we need the key to be in ppk form.
   >Refer [this](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/putty.html) link for detailed proceduring of connecting
   >with putty.
3. Connect with the ec2 instance using putty.
   > Default user name is <strong>ubuntu</strong>
4. Use [WinSCP](https://winscp.net/eng/index.php) to transfer our files to our remote ec2 instance.
   > In WinSCP the login can be done using the saved configuration from Putty.\
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
   1. To create a python virtual environment we need venv package, to install
      ```
      sudo apt install python3-venv
      ```
   2. To create virtual env goto project directory then,
      ```
      python3 -m venv venvwetube
      ```
   3. To activate our virtual environment
      ```
      source venvwetube/bin/activate
      ```
   4. To deactivate and get back to global environment
      ```
      deactivate
      ```
7. Install the following packages required inside the virtuak env
   ```
   python3 install Flask==2.3.2
   ```
   ```
   python3 install Flask-Cors==4.0.0
   ```
8. to run the server locally,
   ```
   python3 server.py
   ```
## Exposing to the internet
1. install apache
   ```
   sudo apt-get install apache2
   ```
   > check if the apache server works by accessing the public DNS of ec2 instance.
2. install wsgi
   ```
   sudo apt-get install libapache2-mod-wsgi-py3
   ```
3. 
### Status Codes
1. 304 - The "304 Not Modified" status code is returned when the client (usually a web browser) makes a request for a resource that the server considers to be unchanged since the last time it was requested. The server then sends a response indicating that the client's cached version of the resource is still valid and can be used.
This behavior is due to the client sending an If-Modified-Since header in its request, indicating the timestamp of the version it currently has cached. If the server determines that the resource hasn't been modified since that timestamp, it returns a "304 Not Modified" response instead of the actual content, saving both bandwidth and processing time.
