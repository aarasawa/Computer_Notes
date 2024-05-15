#Cipher #EncryptionAlgorithm #TranspositionCipher

Source: [link](https://www.boxentriq.com/code-breaking/rail-fence-cipher)

Also known as the *zigzag* cipher from how the letters are arranged. It encrypts text by writing them in order in a diagonal up-down pattern. The number of *rails* is the number of rows to designate per diagonal from top to down. 

*Example*: ABCDEFGHIJ
```
row 1:  A          G
row 2:    B      F  H
row 3: 	    C  E     I
row 4: 	      D       J
```
In this example, the *number of rails is 4.* Hence why there are 4 rows of letters per diagonal. To find the ciphertext, go from the top row to the bottom follow along horizontally per row until there are no more letters in the column. ABCDEFGHIJ -> AG + BFH + CEI + DJ = AGBFHCEIDJ

There is another option for encrypting: the *offset*. It determines how many rows you skip before starting the ciphertext. Because the pattern does not start to alter until an offset of 1, to totally slip the plaintext, an offset of *# rails - 1* is needed.  It then follows that an offset of *(# rails - 1) x 2* returns us to the original pattern. 
```
# an offset of 3, with the number of rails = 4 would look like this
row 1:        D        J
row 2:      C  E      I
row 3:    B      F  H
row 4:  A          G
```
