# Here are the steps to installing and setting up GDB on Mac OS Sierra/High Sierra. Run brew install gdb. On starting gdb, you will get the following error:

## Unable to find Mach task port for process-id 2133: (os/kern) failure (0x5).
 (please check gdb is codesigned - see taskgated(8))
To fix this error, follow the following steps:

Open Keychain Access
In menu, open Keychain Access > Certificate Assistant > Create a Certificate
Give it a name (e.g. gdbcert)
Identity type: Self Signed Root
Certificate type: Code Signing
Check: Let Me Override Defaults
Continue until "Specify a Location For"
Set Keychain location to System. If this yields the following error: Certificate Error: Unknown Error =-2,147,414,007 Set Location to Login, Unlock System by click on the lock at the top left corner and drag and drop the certificate gdbcert to the System Keychain.
Create certificate and close Certificate Assistant.
Find the certificate in System keychain.
Double click certificate.
Expand Trust, set Code signing to Always Trust
Restart taskgated in terminal: killall taskgated
Enable root account by following the steps given below: Open System Preferences. Go to User & Groups > Unlock. Login Options > "Join" (next to Network Account Server). Click "Open Directory Utility". Go up to Edit > Enable Root User.
Codesign gdb using your certificate: codesign -fs gdbc /usr/local/bin/gdb
Shut down your mac and restart in recovery mode (hold down command-R until apple logo appears)
Open terminal window
Modify System Integrity Protection to allow debugging: csrutil enable --without debug
Reboot your Mac. Debugging with gdb should now work as expected.
