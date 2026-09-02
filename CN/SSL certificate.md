
## Hybrid encryption -

for data encryption - 
- client sym key encryption use karta h for encrypting the actual data.
- vo sym key server tak dene ke lie  ( client - server ) asym key use karte hai

1. server apni asym public key client ko dega
2. client ek sym key gen karke mili hui public key se encrypt karke server ko de dega
3. server asym private key ka use karke un encrypt karega -- ( now, server gets the sym key gen by client )
4. client ab apna actual data gen. sym key se encrypt karke send kar dega and server uska same key se un encrypt kar sakta h

## Problem -
- starting m jab server apni asym public key share karega to client
- tab hacker beech m rehkar problem kar sakta h -- like --> server ki key rok kar apni public key de dega client ko
- NOTE - hacker public key tamper nahi kar sakta due to Public Key Infrastructure (PKI) security (tabhi vo apni alag ki hi de deta h)
- and jab client usse apni gen sym key share karega to vo hacker ko mil jaegi

## Solution -
- server apni public key ko certify karvata hai ek verified party se. ( ye party ko technical terms m `CA - Certificate Authority` bola jata h)
- vo certificate m ---> `server's public key` and `signature = party's public key + server public` key rehta h.
- ab client naively jo bhi public key mili usse apni sym key gen nahi karega directly
- instead, pehle us party ko reach karke bolega ki ek public key mili hai jo aapne certify kari h
- or us party ki public key unse le lega
- ab party public key and jo server public key aai thi unko mila ke signature gen karega and certificate wale signature se match karega
- if signature valid hoga that means server's public key fake nahi hai and authentic hai


## NOTE -
Public Key Infrastructure (PKI) aur SSL/TLS ki security aisi banayi gayi hai ki hacker certificate mein koi bhi phair-badal (tampering) nahi kar sakta.


---

## SSL / TLS (Secure socket layer / transport layer security)-
- these are cryptographic protocols designed to provide secure communication over a network.
- TLS is successor of SSL and now-a-days TLS only is used.
- however, everyone uses SSL as a general term still.


## CIA triad -
TLS ensures CIA

- certificate ---used for--->   authentication
- data encryption   ---used for---->   confidentiality
- hashing ---used for----> integrity (means data is not modified in between)