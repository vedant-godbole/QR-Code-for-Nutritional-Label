# Winter22-qr-code-design
## --- Backend Team ---
## Text Extraction Process From Images 
<p align="justify"> 
<ul>
  <li> Loop through each image file in the list: This code loop through a list of image file names and process each image one by one. Create an empty list to store nutritional data of the current image: This creates an empty list where we will store the nutritional data extracted from the current image. Read and resize the image: The code reads an image file using OpenCV and resizes the image to a larger size. Convert the image to RGB format: This converts the image from BGR format (which OpenCV uses) to RGB format (which PyTesseract uses). </li> 
  <br>
  <li> Define the custom configuration for PyTesseract OCR: The code sets some custom configuration options for the PyTesseract OCR engine, including the language, page segmentation mode, and a whitelist of characters to recognize. Extract the text data from the image using PyTesseract OCR with custom configuration: This uses PyTesseract to extract the text data from the resized and converted image using the custom configuration defined earlier. </li>
  <br>
  <li> Create a Pandas dataframe from the extracted data: The extracted text data is converted into a Pandas dataframe for easier processing. Clean up blanks, remove lines with no text and no confidence score: This removes any lines from the dataframe that do not have any text or have a confidence score of -1 (meaning the OCR was unable to recognize the text). Sort the text blocks vertically: This sorts the remaining text blocks in the dataframe in vertical order. </li>
  <br>
  <li> Loop through each block of text and extract the text data: This loops through each text block in the sorted dataframe and extracts the text data by combining individual characters into words and lines of text. Extract the nutritional data from the text data: This extracts the nutritional data from the text data by searching for specific keywords or patterns in the text. Append the nutritional data of the current image to the table list: The extracted nutritional data for the current image is appended to a list of nutritional data for all the processed images. </li>
  <br>
</ul>
</p>

## Database Connectivity
<p align="justify"> <b> Inserting Data into Database: </b> </p>
<ul>
<li><p align="justify">First, the pandas library is used to read the CSV file 'products_data_db.csv' and store the data in a dataframe called 'df'.</p></li>
<li><p align="justify">Then, only the first 15 columns are selected using the iloc method and the dataframe is updated.</p></li>
<li><p align="justify">The code then creates a connection to an SQLite database named 'mydatabase.db' using the connect method from the sqlite3 library.</p></li>
<li><p align="justify">Next, a cursor object is created using the cursor method on the connection object.</p></li>
<li><p align="justify">The table is created with the column names specified in the 'columns' list, and the Serial_Number column is set as the primary key using a CREATE TABLE query.</p></li>
<li><p align="justify">The to_sql() function from pandas is used to insert the data from the 'df' dataframe into the 'mytable' table in the database. The 'if_exists' parameter is set to 'append' so that the data is added to the existing table.</p></li>
</ul>
<p align="justify"> <b> Retrieving Data from Database and Inserting into Dataframe: </b> </p>
<ul>
<li><p align="justify">A SELECT query is executed on the cursor object to retrieve all the rows from the 'mytable' table in the database.</p></li>
<li><p align="justify">The fetchall() method is used to retrieve all the rows of the result set.</p></li>
<li><p align="justify">The code then iterates over each row in the result set, converts the row to a list, and appends the list to another list called 'rows_copy'.</p></li>
<li><p align="justify">The list of rows is printed to the console.</p></li>
<li><p align="justify">Finally, the data is inserted into a new pandas dataframe by passing 'rows_copy' to the pandas DataFrame() constructor.</p></li>
<li><p align="justify">Note that in this specific code, the column data types are all set to 'TEXT' in the CREATE TABLE query, which might not be appropriate for some columns. In a real-world application, it's important to make sure that the data types match the intended data.</p></li>
</ul>

## QR Code Generator
<p align="justify">
  <ul>
<li>The OpenCV library is imported for image processing.</li>
<li>The pandas library is imported for working with dataframes.</li>
<li>The qrcode library is imported for generating QR codes.</li>
<li>A URL is defined to be encoded in the QR codes.</li>
<li>An Excel file 'Products-Data.xlsx' is read into a pandas dataframe. If the file is not found, an error message is printed to the console and the program is exited.</li>
<li>The column names of the dataframe are extracted and stored in a variable called cals.</li>
<li>A loop is used to iterate over the rows in the dataframe. For each row:</li>
<ul>
<li>The data for the row is stored in a dictionary called data.</li>
<li>An empty string encoded_data is created to store the data.</li>
<li>Another loop is used to iterate over the keys and values of data. For each key-value pair:</li>
<ul>
<li>If the index of the key is less than 15, the key and value are appended to encoded_data string.</li>
</ul>
<li>A QR code object is created with the specified properties: version 1, error correction level of L, box size of 4, and border size of 4.</li>
<li>The data is added to the QR code object with the URL and encoded_data.</li>
<li>The QR code image is generated using the make_image() method.</li>
<li>The QR code image is saved to a file with a unique name based on the row index using the save() method.</li>
</ul>
</ul>
  </p>
  
## Usage Of OPENCV + PYTESSERACT Custom Configurations For Extracting Data From Images
<p align="justify">
  <ul>
<li>OpenCV is used to read and resize the images before performing OCR using pytesseract. </li>
<li>OpenCV is a powerful computer vision library that can be used to read, manipulate, and analyze images and videos. </li>
<li>In this code, OpenCV's cv2.imread() function is used to read the images and cv2.resize() function is used to resize the images to a larger size, so that the text in the images can be more easily read by the OCR engine. </li>
<li>Additionally, the cv2.cvtColor() function is used to convert the images from BGR to RGB format, which is the format that is required by pytesseract. </li>
<li>Overall, OpenCV provides several useful image processing functions that can be used in combination with OCR to extract text from images.</li>
<li>If OpenCV is not used to preprocess the image before passing it to pytesseract, the OCR engine may not be able to accurately recognize the text in the image. </li>
<li>The custom_config variable defines a custom configuration for pytesseract OCR (Optical Character Recognition) engine that is used to extract text from images. </li>
<li>The configuration consists of the following components: 
  <ul>
  <li>-l eng: specifies the language used in the text. Here, it is set to 'eng' for English language.</li>
  <li>--oem 3: specifies the OCR Engine Mode. Here, it is set to 3, which means using the default LSTM OCR engine.</li>
  <li>--psm 6: specifies the Page Segmentation Mode. Here, it is set to 6, which means assume a single uniform block of vertically aligned text.</li>
  <li>-c tessedit_char_whitelist="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-:.$%./@& *": specifies a whitelist of characters that pytesseract should recognize. Here, it includes capital and lowercase English alphabets, numbers, some special characters like hyphen, colon, dollar sign, percentage sign, forward slash, at sign, ampersand, and an asterisk.</li>
  </ul>
</li>
<li>By using this custom configuration, we can fine-tune the OCR engine to better recognize the specific types of characters present in the images, and improve the accuracy of the text recognition process.</li>
</ul>
  </p>
  <br>
  
## Collected Images Of Various Products(IIITD Canteen, Shops)
<a href= "https://drive.google.com/drive/folders/14zI4QJFr_8ktiqnRzWRW4T-Cbk4YPcR6?usp=share_link"> To View Images Click Here</a>

## --- Web Application Development Team ---
## Tech stack used - ReactJS + Django + HTML + CSS + JS +Sqlite
<p align='justify'>
For web application development, we have used ReactJS for frontend development and Django for backend development. ReactJS framework helps us to create a responsive and scalable front end side of web application. Meanwhile, Django framework helps us in creating a backend framework quickly and effectively. With Django, we have used REST Framework for creating HTTP Methods like GET,DELETE,POST. For database, we have used dbsqlite3 which is provided by django framework.
  
## Application Workflow
  <img src="https://github.com/cosylabiiit/Winter22-qr-code-design/blob/main/Basic%20workflow%20IP.png?raw=true"
     alt="Markdown Monster icon"
     style="float: left; margin-right: 10px;" />
  
 ## Front End Workflow
  <ul>
    <li> The user scans the QR-code for the packaged food product which leads him to the webpaged mapped to the product ID.  </li>
    <li> The user can see the nutrition table and the nutrition pie chart.  </li>
    <li> Navigation bar contains the following features - Home, Calculator,FAQs, Contact Us, CoSyLab, Sign In  </li>
    <li> Sign In button leads the user to google login page. Upon login the user can calculate his BMR and log his product consumption for the day. </li>
    <li> The logged product entries gets deleted at 11:59 PM everyday.   </li>
    <li> If the user is not logged in, he cannot use the calculator and thus cannot log his daily product consumption.    </li>
    </ul>
  
  
 ## Back End Workflow
  We have used Model, View, Template(MVT) architecture in django backend. 
  <ul>
    <li> Model defines the schema that has to be used in the database table.</li>
    <li> View defines HTTP requests for APIs. In our project, we have created 4 APIs:
      <br>
      1. GET Request- To fetch the nutrition details of any product based on its ID. https://cosylab.iiitd.edu.in/qr-code-design-api/nutritionApi/v1/details/:id
      <br>
      2. GET Request- To fetch the food consumed history of a particular user from database. https://cosylab.iiitd.edu.in/qr-code-design-api/calorie-count/<str:userEmail>/
      <br>
      3. POST Request- To upload user details to the database, which includes user's latest Basal Metabolic Rate, Calories consumed etc. https://cosylab.iiitd.edu.in/qr-code-design-api/saveCalorieDetails/
      <br>
      4. DELETE Request- To delete user details from database. https://cosylab.iiitd.edu.in/qr-code-design-api/calorie_details/
      <br>
     <li> Template defines HTML pages which are to be rendered. We have not used HTML pages from template, instead we have used React framework.
        <br>
  </ul>
      
   
