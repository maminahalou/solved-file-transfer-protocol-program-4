Download Link: https://assignmentchef.com/product/solved-file-transfer-protocol-program-4
<br>
<h1>Program Description</h1>

You will write the <strong>Server        </strong>and<strong>      </strong>the<strong>       Client</strong> programs that run a simplified <strong>File Transfer Protocol</strong> for transferring files. The Server must be able to handle multiple clients simultaneously and listen on <strong>port    5521</strong> (control connection) for file transfer requests. Once a request is accepted, the Server opens <strong>another</strong> <strong>port          </strong>(data connection)<strong>      </strong>for the Client to establish the connection dedicated for file transfer (you can use 5520 or any port numbers between 5500-5540.) The data connection should be closed after the file transfer is done. However, the control connection must remain connected until the Client is disconnected. Each Client should be handled with a separate thread.

<h1>The Protocol</h1>

The simplified FTP supports only two commands: <strong>GET</strong> <strong>[filename]     </strong>and <strong>PUT          [filename]</strong>. A GET command transfers a file from the Server to the Client, and a PUT command transfers the file from the Client to the Server. The Client will initiate the connection and send either a GET or PUT command. The sequence of interactions between the Server and Client are summarized as follows.

<ol>

 <li><strong>Client:</strong> connect to the Server through the control connection 5521.</li>

 <li><strong>Server:</strong> accept the connection and send the list of files available for download to the Client.</li>

 <li><strong>Client:</strong> the UI displays the list of files from the Server. The Client sends either GET or PUT command as a request to download/upload the selected file, one at a time.</li>

 <li><strong>Server:</strong> receive the request, open a data connection dedicated to the file transfer, and send the port number to the Client. Close the data connection once the file transfer is done.</li>

 <li><strong>Client:</strong> use the specified port number to contact the Server for the file transfer, and close the data connection once the file transfer is done. Client UI must refresh and show the updated list of files. The Client can send another request through the control connection, or disconnect from the Server.</li>

</ol>

The following screen shots are sample Client UI with sample runs and the sample Server system output. You must use a <strong>JList    </strong>to list the remote files in the folder <strong>Files</strong> from the Server, and a <strong>JList</strong> to list the local files from the Client’s current folder.

<h1>Program Requirement</h1>

<ol>

 <li>The Server’s system output must show the Server is currently running, and display all file transfer activities. You must try-catch everything and display appropriate error messages identifying the specific exception. The Server must not crash under any situations.</li>

 <li>The Server must include 2 classes: <strong>FTPServer </strong>class and <strong>FTPThread </strong> You must use <strong>JFrame</strong> for the Client program. All files must be sent in <strong>1024-byte          chunks</strong>. Follow the instructions below.</li>

 <li>You must schedule a demo by sending me an email. After the demo, you must zip all files for Program 4 and submit the zip file to the Program 4 Dropbox on D2L by the due date.</li>

</ol>

<h1>v Server     Program</h1>

<strong>FTPServer     class</strong> will be multi-threaded, where the processing of each incoming request will take place inside a separate thread of execution (<strong>FTPThread</strong>). You must have a <strong>run()</strong> method<strong>     </strong>in FTPServer class.<strong>                   </strong>

<strong>FTPThread            class</strong> implements a proprietary File Transfer Protocol that handles file transfers to/from the

Clients.

This class extends Java Thread class and you must implement the <strong>run()</strong> method that handles the file transfer. You must implement and use the following <strong>private         methods</strong>.

<ul>

 <li><strong>listFiles()</strong> – retrieve all file names (excluding folders) from the folder <strong>Files</strong> and send a list of file names with a single String instance to the Client socket. Here are some useful methods.</li>

</ul>

File dir = new File(“Files”);   // create a new instance of File class and set the pathname File [] files = dir.listFiles();   // get the list of all files files[i].isFile()  // returns true if files[i] is a file NOT a folder files[i].getName()  //returns the file name as a String

<ul>

 <li><strong>sendFile(String </strong>filename<strong>)        </strong>– send the file <strong>filename</strong> thru the data connection. The file path will be <strong>“Files\” + filename</strong>, if the folder <strong>Files  </strong>contains the file. You must use double back-slash because a single back-slash identifies a control character next to it.</li>

 <li><strong>getFile(String </strong>filename<strong>) </strong> – receive the file <strong>filename</strong> thru the data connection. The file path will be <strong>“Files\” + filename</strong>, if the file is to be stored in the folder <strong>Files</strong>.</li>

</ul>

<h1>v Client      Program</h1>

You must use <strong>JFrame</strong> and include the following components.

<ul>

 <li><strong>JTextField </strong>for host IP/name and port number, and a <strong>JButton</strong> to connect/disconnect to/from the Server.</li>

 <li><strong>JList</strong> for displaying the remote files on the Server and the local files on the Client.</li>

 <li><strong>JButton </strong>for sending the GET or PUT command.</li>

 <li><strong>JTextArea</strong> for displaying messages and the interactions between Client/Server.</li>

</ul>

When you bring up your Client, the local files must be automatically loaded to the JList. When the connect button is clicked, the remote files must be displayed on the JList. You must implement the following <strong>private       methods</strong>.

<ul>

 <li><strong>listRemoteFiles() </strong>– read the String sent from the Server, and use <strong>StringTokenizer</strong> to decompose the file names. Create an instance of Vector class and add all file names to the list. To export the names from the Vector to the JList, use <strong>.setListData(Vector   </strong>v<strong>)</strong></li>

 <li><strong>listLocalFiles() </strong>– retrieve filenames from the local folder and list all files on the JList. Use an instance of Vector class to manage the list.</li>

 <li><strong>sendFile(String </strong>filename<strong>)        </strong>– send the file <strong>filename</strong> thru the data connection.</li>

 <li><strong>getFile(String </strong>filename<strong>) </strong> – receive the file <strong>filename</strong> thru the data connection.</li>

</ul>

<strong>Program Grading – </strong>your grade will be posted within 5 business days after the due date.

<table width="564">

 <tbody>

  <tr>

   <td width="360"><strong>Exceptions/Violations </strong></td>

   <td width="108"><strong>Each Offense </strong></td>

   <td width="97"><strong>Max Off </strong></td>

  </tr>

  <tr>

   <td width="360">Program not running</td>

   <td width="108">20</td>

   <td width="97">20</td>

  </tr>

  <tr>

   <td width="360">Failed to transfer files between Client and Server</td>

   <td width="108">20</td>

   <td width="97">20</td>

  </tr>

  <tr>

   <td width="360">Failed to handle multiple connections</td>

   <td width="108">5</td>

   <td width="97">5</td>

  </tr>

  <tr>

   <td width="360">Improper list of files of Server/Client on UI</td>

   <td width="108">3</td>

   <td width="97">6</td>

  </tr>

  <tr>

   <td width="360">File transfer activities are not displayed properly</td>

   <td width="108">2</td>

   <td width="97">6</td>

  </tr>

  <tr>

   <td width="360">Exceptions not caught and handled</td>

   <td width="108">2</td>

   <td width="97">6</td>

  </tr>

 </tbody>

</table>


