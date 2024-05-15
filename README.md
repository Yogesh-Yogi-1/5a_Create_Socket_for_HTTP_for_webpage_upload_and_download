# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## NAME : V.YOGESH
## REG NO : 212223230250
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## PROGRAM
```
import socket

def send_request(host,port,request):
    with socket.socket(socket.AF_INET,socket.SOCK_STREAM) as s:
        s.connect((host,port))
        s.sendall(request.encode())
        reponse=s.recv(4096).decode()
    return response

def upload_file(host,port,filename):
    with open(filename,'rb') as file:
        file_data=file.read()
        content_length=len(file_data)
        request=f"POST /upload HTTP/1.1\r\nHost: {host}\r\nContent-Length: {content_length}\r\n\r\n{file_data.decode()}"
        response=send_request(host,port,request)
    return response

def download_file(host,port,filename):
    request=f"GET /{filename} HTTP/1.1\r\nHost: {host}\r\n\r\n"
    response=send_request(host,port,request)

    file_content=response.split('\r\n\r\n',1)[1]
    with open(filename, 'wb') as file:
        file.write(file_content.encode())

if __name__=="__main__":
    host='example.com'
    port=80

    upload_response=upload_file(host,port,'MyFile.txt')
    print("Upload response:",upload_response)

    download_file(host,port,'MyFile.txt')
    print("File download successfully.")
```
## OUTPUT
![Screenshot 2024-05-15 230654](https://github.com/Yogesh-Yogi-1/5a_Create_Socket_for_HTTP_for_webpage_upload_and_download/assets/148514598/50282e50-a850-4a72-8511-8888a96a94bd)

## RESULT
Thus the socket for HTTP for web page upload and download created and Executed
