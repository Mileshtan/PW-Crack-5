# PW-Crack-5
Cylab CTF PW Crack 5

Q: Can you crack the password to get the flag? Download the password checker here https://challenge-files.cylabacademy.net/library/a2b32b2b4b000d12f209c65a2c414ede32d08a63774f7e150e3e30a3892a386d/level5.py
 and you'll need the encrypted flag https://challenge-files.cylabacademy.net/library/a2b32b2b4b000d12f209c65a2c414ede32d08a63774f7e150e3e30a3892a386d/level5.flag.txt.enc
 and the hash https://challenge-files.cylabacademy.net/library/a2b32b2b4b000d12f209c65a2c414ede32d08a63774f7e150e3e30a3892a386d/level5.hash.bin
 in the same directory too. Here's a dictionary https://challenge-files.cylabacademy.net/library/a2b32b2b4b000d12f209c65a2c414ede32d08a63774f7e150e3e30a3892a386d/dictionary.txt
 with all possible passwords based on the password conventions we've seen so far.

 Hint1: Opening a file in Python is crucial to using the provided dictionary.

 Hint2: You may need to trim the whitespace from the dictionary word before hashing. Look up the Python string function, strip

 Hint3: The str_xor function does not need to be reverse engineered for this challenge.

 Step1: Download all the files
 wget https://challenge-files.cylabacademy.net/library/a2b32b2b4b000d12f209c65a2c414ede32d08a63774f7e150e3e30a3892a386d/level5.py
 wget https://challenge-files.cylabacademy.net/library/a2b32b2b4b000d12f209c65a2c414ede32d08a63774f7e150e3e30a3892a386d/level5.flag.txt.enc
 wget https://challenge-files.cylabacademy.net/library/a2b32b2b4b000d12f209c65a2c414ede32d08a63774f7e150e3e30a3892a386d/level5.hash.bin
 wget https://challenge-files.cylabacademy.net/library/a2b32b2b4b000d12f209c65a2c414ede32d08a63774f7e150e3e30a3892a386d/dictionary.txt

 Step2: Open level5.py in any IDE and make following changes
 
flag_enc = open('level5.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level5.hash.bin', 'rb').read()
key=open('dictionary.txt', 'r').read()
key_list=key.strip()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_5_pw_check():
    for user_pw in key_list:
        user_pw_hash = hash_pw(user_pw)
        if( user_pw_hash == correct_pw_hash ):
            print("Welcome back... your flag, user:")
            decryption = str_xor(flag_enc.decode(), user_pw)
            print(decryption)
            return
        else:
            pass


Step3: Run level5.py
python3 level5.py
and enter password 443b

Step6: Final answer: 
