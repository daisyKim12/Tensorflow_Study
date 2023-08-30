## Upload
To upload a file from your local desktop to Google Colab, you can use the following steps:

### Mount Google Drive
 If you want to persistently store the uploaded files, you can mount your Google Drive in Colab. This step is optional, but it's useful for keeping your uploaded files across sessions.

 ```
 from google.colab import drive
drive.mount('/content/drive')
 ```


### Upload file from desktop
Use the following code to upload files from your local desktop to the Colab environment.
 ```
 from google.colab import files
uploaded = files.upload()
 ```

 After running this code, you'll see a "Choose Files" button. Click it and select the file(s) you want to upload from your desktop. The uploaded files will be available in the current Colab session.


 ### Access Uploaded File
 The uploaded files will be stored in the uploaded dictionary. You can access the files using their keys, which correspond to the filenames. For example:
 ```
 uploaded_filename = 'example.txt'  # Replace with the actual filename
if uploaded_filename in uploaded:
    content = uploaded[uploaded_filename].decode('utf-8')
    print(content)
else:
    print(f"{uploaded_filename} not found in uploaded files.")
```