For protect the important data. We need to encrypt the information.

Insert encrypted data:
`INSERT INTO staff (staff_id, last_name, first_name, email, password) VALUE ("1", "Chan", "Bob", "bob@email.com", AES_ENCRYPT('12345', 'Staff password'));`{{execute}}

Show decrypted data:
`SELECT CAST(AES_DECRYPT(password, 'Staff password') as char(100)) from staff;`{{execute}}

After decrypted the message. We can see the original data.
