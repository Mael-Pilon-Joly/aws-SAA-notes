SSE-S3 (S3 Managed Keys): Amazon S3 handles the encryption and decryption process automatically. Each object is encrypted with a unique key, and the keys themselves are encrypted with a master key that is regularly rotated by AWS.

SSE-KMS (AWS Key Management Service): This uses AWS KMS to manage encryption keys, providing additional control and audit capabilities. It allows you to create and manage encryption keys and also integrates with AWS CloudTrail for monitoring (autiding of when keys were used and by whom).

SSE-C (Customer-Provided Keys): You provide your own encryption keys, and AWS uses them to encrypt your data. AWS doesn't store your keys; you must provide them with each data retrieval request.