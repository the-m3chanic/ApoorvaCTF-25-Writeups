# archbtw [Forensics]

Analysing the pcap we see that its a hid capture provided

extarcting all the usb hid data using tshark i used a script to decode the keycodes to get the following command 

```
nvim flag.txt
:%s/0/10101/g
:%s/1/10011/g
:%s/[01]/\=system("awk 'NR % 2 == ".(submatch(0) == "0" ? "0" : "1")."' synoonyms.txt | shuf -n1")/g
```

we see that this is how the flag.txt given in the handout was generated writing a script to reverse engineer the following :

using this mainly
```py
binary_string = ""
        for word in encrypted_content:
            if word in even_words:
                binary_string += "0"
            elif word in odd_words:
                binary_string += "1"
            else:
                print(f"Warning: '{word}' not found in either word list.")

        binary_string = binary_string.replace("10101", "0")
        binary_string = binary_string.replace("10011", "1")
```
and getting the binary as 
```
Original binary:
011000010111000001101111011011110111001001110110011000110111010001100110011110110110111001100101001100000111011000110001011011010101111100110001011100110101111101100010001100110111010001110100001100110111001001111101
```

now after replacing and decoding the binary we get the flag as 

```
apoorvctf{ne0v1m_1s_b3tt3r}
```