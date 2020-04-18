# Here are the steps to installing and setting up GDB on Mac OS Sierra/High Sierra. Run brew install gdb. On starting gdb, you will get the following error:

` Unable to find Mach task port for process-id 2133: (os/kern) failure (0x5).`

## (please check gdb is codesigned - see taskgated(8))
__To fix this error, follow the following steps:__

- [x] Open Keychain Access
- [x] In menu, open Keychain Access > Certificate Assistant > Create a Certificate
- [x] Give it a name (e.g. gdbcert)
- [x] Identity type: Self Signed Root
- [x] Certificate type: Code Signing
- [x] Check: Let Me Override Defaults
- [x] Continue until "Specify a Location For"
  - Set Keychain location to System. If this yields the following error: Certificate Error: Unknown Error =-2,147,414,007 Set   - Location to Login, Unlock System by click on the lock at the top left corner and drag and drop the certificate gdbcert to the System Keychain.
- [x] Create certificate and close Certificate Assistant.
- [x] Find the certificate in System keychain.
- [x] Double click certificate.
- [x] Expand Trust, set Code signing to Always Trust
- [x] Restart taskgated in terminal: killall taskgated
- [x] Enable root account by following the steps given below: Open System Preferences. Go to User & Groups > Unlock. Login Options > "Join" (next to Network Account Server). Click "Open Directory Utility". Go up to Edit > Enable Root User.
- [x] Codesign gdb using your certificate: codesign -fs gdbc /usr/local/bin/gdb
- [x] Shut down your mac and restart in recovery mode (hold down command-R until apple logo appears)
- [x] Open terminal window
- [x] Modify System Integrity Protection to allow debugging: csrutil enable --without debug
- [x] Reboot your Mac. Debugging with gdb should now work as expected.
