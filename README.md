# ssh-key-based-authentication-linux
This project demonstrates how to configure SSH key-based authentication to enable secure, passwordless login between Linux servers using public-keycryptography.

🚀 Overview

This project demonstrates how to set up secure, passwordless SSH login between two Linux machines using SSH key pairs.

Instead of entering a password every time, authentication is handled using a private–public key mechanism, making remote access faster and more secure.

🎯 Objective

Enable a user (feb15) to connect from one Linux server to another without typing a password.

🧠 How It Works
  - A key pair is generated on the client machine
  - The public key is copied to the remote machine
  - The remote server trusts the client using this key
  - Authentication happens automatically using cryptography
    
🏗️ Architecture Flow
[ Client Machine ]
      |
      |  (Public Key)
      |-----------------------> 
      |                        [ Remote Machine ]
      |                        (authorized_keys)
      |
      | <---- Passwordless SSH Access ----

      
⚙️ Step-by-Step Implementation
* Step 1: Generate SSH Key Pair (Client)
      [ssh-keygen -t rsa]
Press Enter for default location
Optionally set passphrase (or leave empty)

✅ This creates:

  - id_rsa → Private key (keep safe 🔒)
  - id_rsa.pub → Public key (shareable 📤)
  
* Step 2: Verify Key Generation
    cd ~/.ssh
    ls -latr

You should see:
    - id_rsa
    - id_rsa.pub
    - known_hosts
* Step 3: View Public Key
    - cat id_rsa.pub

This is the key that will be shared with the remote server.

*  Step 4: Copy Public Key to Remote Server
scp id_rsa.pub feb15@192.168.125.141:~
Enter password once
File gets transferred successfully

*  Step 5: Configure SSH on Remote Server

Login to remote system and run:

  - mkdir ~/.ssh
  - chmod 700 ~/.ssh
  - cp id_rsa.pub ~/.ssh/
  - cd ~/.ssh
  - mv id_rsa.pub authorized_keys
  - chmod 640 authorized_keys
    
* Step 6: Test Passwordless Login

From client:

  - ssh feb15@192.168.125.141

✅ You should log in without entering password

*  Step 7: Run Remote Commands Directly
ssh feb15@192.168.125.141 "uptime; uname -a"

✔ Executes commands remotely without login prompt

📸 Screenshots Breakdown:

📷 1. SSH Key Generation
- Shows execution of ssh-keygen -t rsa
- Confirms creation of private & public keys
- Displays fingerprint and randomart image
  
📷 2. .ssh Directory Verification
- Lists contents of .ssh directory
- Confirms:
    - id_rsa
    - id_rsa.pub
    - known_hosts
      
📷 3. Public Key Content
- Output of cat id_rsa.pub
- This key is used for authentication
  
📷 4. Public Key Transfer
- Uses scp to copy key to remote server
- Shows successful file transfer
  
📷 5. SSH Directory Setup (Remote)
- Creation of .ssh directory
- Permission set to 700
- Public key copied into it

📷 6. Renaming the copied public key
- Renaming it to the authorized_keys
- Permission set to 640

📷 7. Connecting the server 2 without password

🔐 Security Best Practices
❌ Never share your private key (id_rsa)

✅ Always set correct permissions:
- chmod 700 ~/.ssh
- chmod 640 ~/.ssh/authorized_keys
  
🔄 Ensure SSH service is running on remote machine

⭐ Key Benefits
- 🚫 No need to type passwords repeatedly
- ⚡ Faster server access
- 🔐 Stronger security than password authentication
- 🤖 Ideal for automation (scripts, deployments)
  
📌 Use Cases
- DevOps automation
- Remote server management
- CI/CD pipelines
- Secure file transfers
  
🎯 Final Thoughts
- SSH key-based authentication is a must-have skill for Linux administrators.
- It improves both security and efficiency, especially when working with multiple servers.
