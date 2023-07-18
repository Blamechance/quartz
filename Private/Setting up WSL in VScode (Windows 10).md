1. Install WSL on microsoft store.

1. Run WSL once finished, to set up the account.

1. Download the “WSL” Extension in VScode — reload the application once finished.

1. Click the bottom left icon to connect to WSL as remote

To open a folder within the windows directory, from within VScode terminal

1. Open VSCode.

1. Click on the Extensions icon on the Activity Bar on the side of VSCode and search for "Remote - WSL".

1. Click the "Remote - WSL" extension to select it.

1. Click the "Reload" button to reload VSCode with the extension.

1. Open a new terminal in VSCode by going to Terminal > New Terminal in the top menu or by pressing Ctrl+\` (backtick).

1. In the terminal, type "code" followed by a space and then the path to the folder you want to open in WSL.
   For example: 
   
   ````
   code /mnt/c/Users/YourUsername/Documents/my_folder
   ````

1. Press Enter to run the command.

1. VSCode will now open the folder in WSL remote mode, allowing you to edit and run Linux files and commands from within VSCode as if you were working directly in a Linux environment.
