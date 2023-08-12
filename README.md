<h1 align="center"> WeTube</h1>
<p align="center"> A video sharing platform where individuals can upload their video along with subtitles on specific timestamps and can view the videos on the platform with subtitles.</p>

### Status Codes
1. 304 - The "304 Not Modified" status code is returned when the client (usually a web browser) makes a request for a resource that the server considers to be unchanged since the last time it was requested. The server then sends a response indicating that the client's cached version of the resource is still valid and can be used.
This behavior is due to the client sending an If-Modified-Since header in its request, indicating the timestamp of the version it currently has cached. If the server determines that the resource hasn't been modified since that timestamp, it returns a "304 Not Modified" response instead of the actual content, saving both bandwidth and processing time.
