# EX-NO-11-ELLIPTIC-CURVE-CRYPTOGRAPHY-ECC

## Aim:
To Implement ELLIPTIC CURVE CRYPTOGRAPHY(ECC)


## ALGORITHM:

1. Elliptic Curve Cryptography (ECC) is a public-key cryptography technique based on the algebraic structure of elliptic curves over finite fields.

2. Initialization:
   - Select an elliptic curve equation \( y^2 = x^3 + ax + b \) with parameters \( a \) and \( b \), along with a large prime \( p \) (defining the finite field).
   - Choose a base point \( G \) on the curve, which will be used for generating public keys.

3. Key Generation:
   - Each party selects a private key \( d \) (a random integer).
   - Calculate the public key as \( Q = d \times G \) (using elliptic curve point multiplication).

4. Encryption and Decryption:
   - Encryption: The sender uses the recipient’s public key and the base point \( G \) to encode the message.
   - Decryption: The recipient uses their private key to decode the message and retrieve the original plaintext.

5. Security: ECC’s security relies on the Elliptic Curve Discrete Logarithm Problem (ECDLP), making it highly secure with shorter key lengths compared to traditional methods like RSA.

## Program:
```
class Point:  
def init(self,x,y): self.x,self.y=x,y 
def mod_inv(a,m):  
m0,x0,x1=m,0,1  
while a>1:  
q=a//m; a,m=m,a%m  
x0,x1=x1 - q*x0,x0  
return x1+m0 if x1<0 else x1 
def point_add(P,Q,a,p):  
if P.x==Q.x and P.y==Q.y:  
num=3P.x**2+a  
den=mod_inv(2P.y,p)  
else:  
num=Q.y-P.y  
den=mod_inv(Q.x-P.x,p)  
lam=(numden)%p  
x_r=(lam**2-P.x-Q.x)%p  
y_r=(lam(P.x - x_r)-P.y)%p  
return Point(x_r,y_r) 
def scalar_mul(P,k,a,p):  
R=P for _ in range(k-1):  
R=point_add(R,P,a,p)  
return R 
p=int(input("p: "))  
a=int(input("a: "))  
b=int(input("b: "))  
G=Point(int(input("G.x: ")),int(input("G.y: ")))  
dA=int(input("Alice priv: "))  
dB=int(input("Bob priv: ")) 
PA=scalar_mul(G,dA,a,p)  
PB=scalar_mul(G,dB,a,p)  
print(f"Alice pub: ({PA.x},{PA.y})")  
print(f"Bob pub: ({PB.x},{PB.y})") 
SA=scalar_mul(PB,dA,a,p)  
SB=scalar_mul(PA,dB,a,p)  
print(f"Alice shared: ({SA.x},{SA.y})")  
print(f"Bob shared: ({SB.x},{SB.y})")  
print("Success" if SA.x==SB.x and SA.y==SB.y else "Fail")
```

## Output:
<img width="655" height="325" alt="image" src="https://github.com/user-attachments/assets/08c8b0b7-dbe2-4dc4-aa78-36a37ba78485" />



## Result:
The program is executed successfully

