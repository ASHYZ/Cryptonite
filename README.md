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


  
ii) Most Cookies ( WEB EXPLOITATION)

 I tried doing this challenge but couldn't solve it.
 As far as I understood this question was that key is one of the cookie name . I tried to study flask functions and learnt that flask_unsign can be used to proceed further as it helps to fetch and decode session cookies of a Flask application by guessing secret keys.
 But I couldn't procced further this.

 
iii)	Filtered Shellcode (BINARY)
My approach for this question was to look at the every function given in that ‘fun’ file. I learned that to analyze for its calling convention and register usage, you would need to disassemble a specific function or code segment within this binary using a disassembler tool such as objdump or gdb (GNU Debugger).
I used  “objdump -d -M intel -j .text binary_file” which led me to the following: 

<img width="944" alt="Screenshot 2023-11-10 190027" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/d334158f-d065-4cb0-bf36-ea7712b33cf8">

I tried looking upon those call functions but couldn’t proceed further.

iv) Hijacking ( BINARY )

 The launched instance gave me 
 username:- picoctf
 password:- w26873vTLt
 saturn.picoctf.net 54961

 I used the following command to SSH into the server
 ssh -p 54961 picoctf@saturn.picoctf.net 

<img width="731" alt="Screenshot 2023-11-15 181914" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/aa237d41-f26d-4405-a783-141bcb611bbd">

 I used ls -al to list all the items inside the directory

 According to the challenge it should have been a python file so I tried to open and run  .server.py

 <img width="608" alt="Screenshot 2023-11-15 181854" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/f2597edc-69a4-4e51-b6f9-091d71c97604">


 Then I tried running sudo -l . It was written that we can run the /usr/bin/vi coomand on challenge so I tried to search upon it and got sudo vi -c ‘:!/bin/sh’ /dev/null commnand which was helpful.

 then the I went into the root directory and got the flag.


<img width="849" alt="Screenshot 2023-11-15 181838" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/d203f52c-7ae9-4f7e-9b67-c5b46be249eb">


 v)	Play Nice (CRYPTOGRAPHY)
      
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



vi) Mini RSA (CRYPTOGRAPHY)

I tried to learn about RSA and learnt about the formula  C ≡ P e (mod N) . I tried modifying the formula according to the need and the implement as we had the values of N,C,e given .


I got a non-readable text which I tried converting into text but couldn't. 

<img width="649" alt="Screenshot 2023-11-15 151255" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/583769d7-257d-4d6a-b9ff-97d8e0e09a2f">


So I changed my approach and tried doing it using cube root attack. since the value of e is very small (3) , there will be not too much power to calculate the cube root of the above expression.

C = P**e % N, now for any integer x we can say:)

P**e = C + N*x => P = (C + N*x)**1/e ,

which means we can actually brute force the value of x. we can take it from range 1,10000 and then calculate P for each x, and check whether it contains ‘pico’ string in it. since the value containing ‘pico’ in it is our flag.

I tried the code given below but for some reasons I am not able to run it in my wsl.
 ~~~
from Crypto.Util.number import long_to_bytes
import gmpy2

# Given values
N = 1615765684321463054078226051959887884233678317734892901740763321135213636796075462401950274602405095138589898087428337758445013281488966866073355710771864671726991918706558071231266976427184673800225254531695928541272546385146495736420261815693810544589811104967829354461491178200126099661909654163542661541699404839644035177445092988952614918424317082380174383819025585076206641993479326576180793544321194357018916215113009742654408597083724508169216182008449693917227497813165444372201517541788989925461711067825681947947471001390843774746442699739386923285801022685451221261010798837646928092277556198145662924691803032880040492762442561497760689933601781401617086600593482127465655390841361154025890679757514060456103104199255917164678161972735858939464790960448345988941481499050248673128656508055285037090026439683847266536283160142071643015434813473463469733112182328678706702116054036618277506997666534567846763938692335069955755244438415377933440029498378955355877502743215305768814857864433151287
e = 3
ciphertext = 1220012318588871886132524757898884422174534558055593713309088304910273991073554732659977133980685370899257850121970812405700793710546674062154237544840177616746805668666317481140872605653768484867292138139949076102907399831998827567645230986345455915692863094364797526497302082734955903755050638155202890599808147276605782889813772992918898400408026067642464141885067379614918437023839625205930332182990301333585691581437573708925507991608699550931884734959475780164693178925308303420298715231388421829397209435815583140323329070684583974607064056215836529244330562254568162453025117819569708767522400676415959028292550922595255396203239357606521218664984826377129270592358124859832816717406984802489441913267065210674087743685058164539822623810831754845900660230416950321563523723959232766094292905543274107712867486590646161628402198049221567774173578088527367084843924843266361134842269034459560612360763383547251378793641304151038512392821572406034926965112582374825926358165795831789031647600129008730

# Loop over possible values of x
for x in range(10000):
    # Calculate cubic root using gmpy2.iroot
    M = gmpy2.iroot(ciphertext + N * x, e)[0]
    
    # Check if the recovered message contains the target substring 'pico'
    if b'pico' in long_to_bytes(M):
        print(x)
        print(long_to_bytes(M))
        break
    else:
        print(str(x) + " trying")

~~~

vii) File Types (FORENSICS)

 The file which was provided was a shell archive file so to extract the files from this file I copied everything from to  '#!/bin/sh' to the last in a new file and saved it as extracted.sh file .

 Then opened the new flag file which gave me:-
 
<img width="952" alt="Screenshot 2023-11-15 200417" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/a51b9041-75c7-4cca-b31c-fec9141a093d">

 Then I extracted the file in extracted.flag using the command 'dd if=flag of=extracted_flag bs=1 skip=68'.

 The extracted file gave me this which I couldn't encode it further.

<img width="955" alt="Screenshot 2023-11-15 200339" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/5e537fad-b681-4993-932f-d8139fc6ef59">

 
 viii)	Pcap Poisoning (FORENSICS)
 
 They provided us with a non-readable file which I thought of converting into text through different converters( as I thought that file to be in base64, utf ) but nothing worked out so I started reading it line by line and apparently the flag was already given in the file provided.

 <img width="456" alt="Screenshot 2023-11-10 103523" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/147d913a-0711-4d0f-ae5e-a17fc7d41d43">
 

  ix) Reverse (REVERSE ENGINEERING)
  The answer was straight up given in the provided pdf.

  x) ASCII FTW (REVERSE ENGINEERING)
  I converted the given file into readable text using suitable converter. I saw the alternate characters were written in sequence as a flag

<img width="288" alt="Screenshot 2023-11-15 145109" src="https://github.com/ASHYZ/Cryptonite/assets/123001554/d3791173-75b9-4e96-b188-bde0a075b06f">
  

  
