# Cryptonite

i)	Caas (WEB EXPLOITATION)

I used the link given on the website Cowsay As a Service :
https://caas.mars.picoctf.net/cowsay/{message}
and here I took message as ‘caas’ .  But as it didn’t lead me to anywhere so I tried giving ‘flag’ as the message which again didn’t help much, So I searched up more about Cowsay  ( as I am completely new to it ) and ended up using the following link as my next step 
https://caas.mars.picoctf.net/cowsay/flag ;ls
  which directed me to a page 
 
<img width="277" alt="Screenshot 2023-11-10 102445" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/98546312-9776-418d-9bb5-69eb5ff88400">

I tried gaining knowledge of every term on the page shown and learnt that ‘falg.txt’ should lead me to the flag I wanted so I used 
https://caas.mars.picoctf.net/cowsay/flag ;cat falg.txt
  which led me to the following page and I got my answer

  <img width="410" alt="Screenshot 2023-11-10 103028" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/f2e104fe-2829-46d6-8bf4-bd380b709b44">

 ii)	Pcap Poisoning (FORENSICS)
 
 They provided us with a non-readable file which I thought of converting into text through different converters( as I thought that file to be in base64, utf ) but nothing worked out so I started reading it line by line and apparently the flag was already given in the file provided.

 <img width="456" alt="Screenshot 2023-11-10 103523" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/147d913a-0711-4d0f-ae5e-a17fc7d41d43">
 

 iii)	Play Nice (CRYPTOGRAPHY)
      
  I tried to implement Playfair cipher on the alphabetic 5X5 matrix (excluding J), and obtained the key: - "PLAIFYREBCDGHKMNOSTUVWXYZ" 
  
  <img width="499" alt="Screenshot 2023-11-10 181201" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/bfd22817-ffa9-490a-a28b-c954f049276e">
  
Inputting this key and the text provided to decrypt in the following code: -
~~~
SQUARE_SIZE = 5
def generate_square(key):
    key = key.replace("J", "")  
    key += "ABCDEFGHIKLMNOPQRSTUVWXYZ" 
    key = key[:SQUARE_SIZE * SQUARE_SIZE]  
    matrix = [key[i:i+SQUARE_SIZE] for i in range(0, len(key), SQUARE_SIZE)]
    return matrix
def get_index(letter, matrix):
    for row in range(SQUARE_SIZE):
        for col in range(SQUARE_SIZE):
            if matrix[row][col] == letter:
                return (row, col)
    return (-1, -1) 
def decrypt_pair(pair, matrix):
    p1 = get_index(pair[0], matrix)
    p2 = get_index(pair[1], matrix)
    if p1 == (-1, -1) or p2 == (-1, -1):
        return pair 
    if p1[0] == p2[0]  
        return matrix[p1[0]][(p1[1] - 1) % SQUARE_SIZE] + matrix[p2[0]][(p2[1] - 1) % SQUARE_SIZE]
    elif p1[1] == p2[1]:
        return matrix[(p1[0] - 1) % SQUARE_SIZE][p1[1]] + matrix[(p2[0] - 1) % SQUARE_SIZE][p2[1]]
    else:
        return matrix[p1[0]][p2[1]] + matrix[p2[0]][p1[1]]
            def decrypt_string(s, matrix):
    result = ""
    for i in range(0, len(s), 2):
        result += decrypt_pair(s[i:i + 2], matrix)
    return result
   ciphertext = "v60ufmk7edg4z13h2oyqa9ib58ntwxlrscjp"
  key = "PLAIFYREBCDGHKMNOSTUVWXYZ"
matrix = generate_square(key)
decrypted_text = decrypt_string(ciphertext, matrix)
print(f"Key: {key}")
print(f"Decrypted Text: {decrypted_text}")
~~~ 

which gave me decrypted message: - q60nqch7bmd4x13k2nrexf9zi58usvwwlueaf
I tried running the playfair.py code in WSL but still didn’t get any output.

<img width="662" alt="Screenshot 2023-11-10 181140" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/4147fbaf-5c36-4156-8be0-3d379fe61a33">

iv)	Filtered Shellcode (BINARY)
My approach for this question was to look at the every function given in that ‘fun’ file. I learned that to analyze for its calling convention and register usage, you would need to disassemble a specific function or code segment within this binary using a disassembler tool such as objdump or gdb (GNU Debugger).
I used  “objdump -d -M intel -j .text binary_file” which led me to the following: 

<img width="944" alt="Screenshot 2023-11-10 190027" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/d334158f-d065-4cb0-bf36-ea7712b33cf8">

I tried looking upon those call functions but couldn’t proceed further.

v) Most Cookies ( WEB EXPLOITATION)

 I tried doing this challenge but couldn't solve it.
 As far as I understood this question was that key is one of the cookie name . I tried to study flask functions and learnt that flask_unsign can be used to proceed further as it helps to fetch and decode session cookies of a Flask application by guessing secret keys.
 But I couldn't procced further this.

  

  
