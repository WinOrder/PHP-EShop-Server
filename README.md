# PHP-EShop-Server
WinOrder online-shop interface (EShop) server example for WinOrder POS written in PHP

You have an online-shop and want to transfer your orders to the WinOrder POS automatically, then you are in the right place!

This is a very simple example for a server-side implementation of the WinOrder EShop interface in PHP.
We don't use a database here, the pending orders are stored as a file on the server.

## TestOrder.php
This PHP script creates a sample order in JSON format. When called (GET), the order is created in JSON format, displayed in the browser and saved as a file in the same directory for later retrieval.
The script shows how to create the syntactically correct JSON format for WinOrder POS from PHP objects.

## GetNewOrders.php
WinOrder POS calls the /GetNewOrders endpoint to retrieve new online orders.
The example script returns all previously created test orders as JSON. For simplicity, all orders are stored as "order_xxx.json" in the same directory.
In real world use you probably use a database.

## SendTrackingStatus.php
After WinOrder has successfully received the JSON data it sends a feedback to your server. This script handles the
"successfully received" feedback, mapped in the JSON with "trackingstatus=0".
In the example, the file of the current online order is deleted. 
In the real use case, you would set the status of the order in your database to "successfully received".

### Testing with WinOrder
You can test the retrieval with a local WinOrder installation:
WinOrder has an integrated WebServer built in, activate it in program settings/Online-Shop/Webserver and set a valid local hostname/IP.
The WWW root is located in the directory "C:\ProgramData\PixelPlanet\WinOrder7\wwwroot".
Load this repository in the subdirectory in the subdirectory "/PHP-EShop-Server".

### Establish the connection in WinOrder

Add a new online store in WinOrder, set the transfer type to "WinOrder (REST)" and the web service URL to the local web server:

Call "http://<local webserver>/PHP-EShop-Server/TestOrder" in the web browser. The call generates a test order and outputs the sample order in JSON format in the web browser.
The order is saved as an "order_xx.json" file in the same directory. The script "TestOrder.php" shows how to create an order in JSON format in PHP.

WinOrder calls the URL endpoint /GetNewOrders in the specified interval. The script GetNewOrders.php searches for JSON files and returns them.
WinOrder reads the JSON orders and reports successful receipt back to the /SendTrackingStatus URL endpoint. The SendTrackingStatus.php script evaluates the status
and looks for the corresponding file and deletes it so that the same order is not transmitted multiple times.
Your server will keep the order in a database and set the status to "received/processed".

For further questions we are at your disposal! Write us an EMail to support@winorder.de, we will help you with the integration!

WinOrder Development Team