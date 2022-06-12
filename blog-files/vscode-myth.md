Date: 12/19/2021

This past quarter, I took [CS 107](http://cs107.stanford.edu) which is an introductory systems course at Stanford. We were required to use the Myth virtual machines at Stanford for the course which meant that we could not access the files locally and edit them using our preferred editors. On the Myth machines, you are required to use a built-in unix-based editor such as Vim or Emacs. While I do recognize the benefits of learning a unix-based editor, it can be nice and more efficient to use a standard text editor such as VS Code. This was how I felt about halfway through the course. After tons of Googling and time lost, it took me a while to get this set up working, but in retrospect, it could have taken ten minutes. Thus, I thought it would be helpful to write a guide for anyone who wishes to do the same and stumbles upon this site. 

## Steps

To get the set up working, first download VS Code and follow the directions enumerated below.  

1. Download the `SSH FS` extension by Kelvin Schoofs in VS Code. 
2. A new icon on your sidebar should appear which allows you to open `SSH FS`. Press this icon and then click the “create a new configuration” button. Name it as you wish. Press “save”. This will open up an “Edit config” file. Keep everything the same except: 
    1. Make `host` equal to `myth.stanford.edu`. 
    2. Make `username` equal to your SUNetID.  
    3. Make `password` equal to your SUNetID password. 
3. You should now see a small little box in the bottom left corner of the window. Click this and select "Add as Workspace folder". Select the remote connection name you made in step 2. 
4. Enter your password (it may ask you twice). 
5. This opens up the folder that is the main root of the entire myth cluster. You should see the directories appear in the toolbar on the left-hand side of the screen. Since we are currently at the root of the entire myth cluster, you would need to click several folders to get to your files in the cluster which is very inconvenient. However, you can bypass this and open up a specific file/folder on the myth machine under your username by pressing `cmd + o` (or `ctrl + o` for Window’s users) and typing in the complete path to the file/folder you wish to edit. To access your directory under your username on the remote Myth machine, you need to specify the path to the root of your directory. To get this path, you could open up a new terminal window and `ssh` as normal into your directory on the virtual Myth machine. Then, type the unix command `pwd` to get your current path. Copy this and paste it into the box in VS Code. You may need to re-enter your password again. 

You should now see all of your files in the toolbar on the left-hand side! You can now edit these files in VS Code. You can compile and run your files by opening up a new, separate terminal or open the built-in VS Code terminal. Now compile and run your files as you normally would. You should always save your edits before compiling and running the programs from the command-line so that the changes persist.

When you are done editing your files on VS Code, press the bottom left box again and press "close remote workspace" to log out successfully. 

Note: you do not need to re-do all of these steps every time. You just need to follow steps 3-5. Conveniently however, when you re-open VS Code you should see a “Recent” tab on the “Get Started” page. Click the remote connection you just set up to open right to your directory on the remote machine. 

I hope this guide was helpful—getting this set up helped me program more efficiently when completing the CS 107 assignments (it was especially helpful for Heap Allocator!). If you have any questions, feel free to email me.
