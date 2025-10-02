# AWS Data Protection Using Encryption

## Overview
In this lab, I worked with **AWS Key Management Service (KMS)** and the **AWS Encryption CLI** to protect sensitive data. The goal was to create a KMS key, use it to encrypt files, and then decrypt them back into readable form.

## Objectives
- Create an AWS KMS encryption key

- Install the AWS Encryption CLI on an EC2 instance  

- Encrypt plaintext files into ciphertext  

- Decrypt ciphertext back to plaintext  

## Steps I Followed

### Create a KMS Key

- Created a **symmetric key** named `MyKMSKey`.  

- Set `voclabs` IAM role as administrator and user.

- Saved the **Key ARN** for later encryption/decryption.  

### Configure File Server

- Connected to the **File Server EC2 instance** via Session Manager.  

- Set up AWS CLI credentials using temporary lab keys. 

- Installed the **AWS Encryption CLI** with pip:  

  ```bash
  pip3 install aws-encryption-sdk-cli
  export PATH=$PATH:/home/ssm-user/.local/bin

### Encrypt and Decrypt Files

- Created test files:

bash
touch secret1.txt secret2.txt secret3.txt
echo 'TOP SECRET 1!!!' > secret1.txt

- Encrypted file:

bash

aws-encryption-cli --encrypt \
  --input secret1.txt \
  --wrapping-keys key=$keyArn \
  --metadata-output ~/metadata \
  --encryption-context purpose=test \
  --commitment-policy require-encrypt-require-decrypt \
  --output ~/output/.

- Verified ciphertext (secret1.txt.encrypted).

- Decrypted back to plaintext:

bash
aws-encryption-cli --decrypt \
  --input secret1.txt.encrypted \
  --wrapping-keys key=$keyArn \
  --commitment-policy require-encrypt-require-decrypt \
  --encryption-context purpose=test \
  --metadata-output ~/metadata \
  --output .

## Results

- secret1.txt was encrypted into unreadable ciphertext.

- The ciphertext was successfully decrypted into secret1.txt.encrypted.decrypted, restoring the original plaintext.

## Key Takeaways

- AWS KMS provides secure key management for encryption workflows.

- The AWS Encryption CLI makes it straightforward to encrypt/decrypt files.

- Using an encryption context strengthens data protection by adding metadata.

## Conclusion

I successfully:

- Created a KMS key

- Configured the File Server

- Encrypted plaintext into ciphertext

- Decrypted ciphertext back into plaintext

This lab gave me practical experience in applying data protection with encryption on AWS.
