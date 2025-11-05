# Deployment

- SignUp on AWS
- Launch an instance
- chmod 400 <secret>.pem( this is for linux and macOs not for windows)
  =>chmod stands for change mode
  =>and 4 means owner can read the file
  =>and 0 means No one else can access.
  =>So, chmod 400 means:“Only the file owner can read this file. Nobody else can read, write, or execute it.”
- write ssh command to connect with the virtual machine on aws.
- Install Node version,similar to the version which is in your local machine.
- Git clone
- ubuntu is case sensitive but windows is not.while deploying the code to production it will throw an error.if the imported file name is not exactly the same with exported file.
