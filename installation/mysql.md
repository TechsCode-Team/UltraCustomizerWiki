## BungeeCord Incompatibility
UltraCustomizer does **NOT** offer bungee compatibility as each command is made for that server specific. It does provide a MySQL storage option to save your data on a database.

UltraCustomizer does offer a share option to make sharing thru server possible more can be found **[HERE](https://guides.ultracustomizer.com/basics/import-export-folders/import-export)**
<br>

## Connecting to MySQL
A MySQL database is used only for store datas. To start your storage process, connect to your server in-game, and open the plugin's GUI by executing the command `/customizer` in chat.
<br>

Then click on the Command Block in the bottom-left of the GUI. *(Called `Settings`)*
<br>

Then click on the EnderChest in the top-middle-right of the GUI. *(Called `MySQL Database`)*
<br>

Then click on the Emerald Block in the middle of the GUI. *(Called `Setup MySQL`)*
<br>

Then click on the Paper in the middle-left of the GUI. *(Called `Credentials`)*
<br>

This will close the GUI and ask you to enter your database's credentials.

Here you will need to fill in the credentials *(info)* of your database. By typing them in the chat in this order:
<br>

- Database IP - Format: 0.0.0.0
- Database Port - Usually: 3306
- Database Name - Depends on what you named your database.
- Database Username - Used to connect to your database.
- Database Password - Used to connect to your database.
<br>

*Here's a shortend version of the MySQL storage process:*
`/customizer >> Settings >> MySQL Database >> Setup MySQL >> Credentials`

Once you have filled in all the credentials, you can now test the connection by clicking on the Emerald Ore in the middle-right of the GUI and confirm it by clicking a second time on the same slot. If your database has not connected or the test takes too long, you have entered the wrong credentials.
<br>

Once you have successfully connected the plugin to your database, restart your server so the connection can be established.
<br>

`TIPS:`
- *If you made an error while entering your credentials, you will have to clear them and re-enter them.*
- *After typing your database credentials for the first time, instead of copying and pasting the same strings again and again, you can press the arrow up key, to go back to the messages you sent, and find your credentials. This will make the installation process much faster and easier.*
