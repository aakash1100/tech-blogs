## The authenticity of host can't be established

#### **When you get such warning?**

If you are a developer, who have used ssh or still using it on daily basis, might have seen following response when you tried to connect to remote machine mostly very *first time*.

```
ssh % ssh -i ~/.ssh/my_private.pem root@0.0.0.0
The authenticity of host '0.0.0.0 (0.0.0.0)' can't be established.
ECDSA key fingerprint is SHA256:abcdABCDefgHIJKlmno+pqrstuvwX=YZ
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```


#### **What is the purpose of this message?**

Assume that the supplied private key (*.pem* file in the example) is correct, but still it is asking to ensure the identity on your own. 

This message is asking for your confirmation before proceeding, because your SSH client is not able to recognize the server (or *SSH host*) you are trying to connect, in other way, it is warning you that you are trying to connect to a server you never connected before. Also, gives a fingerprint which you can use to confirm that whether you are connecting to the correct server or not. 

The SSH client is saying, 

> "Be careful! I don't know with whom you're going to connect, if you are sure, proceed, otherwise verify the fingerprint on your own before proceeding"

Basically, it is trying to keep you safe against security attacks i.e. [Man in the Middle](https://en.wikipedia.org/wiki/Man-in-the-middle_attack). 

Suppose you connect to the server by answering 'yes' to this warning which means your SSH client is now know the server. However, by any chance if your server is reconfigured or in worst case any other server is spoofing the identity of your server, SSH client will be able to warn you before connecting to such server as fingerprints will *not* match this time.


#### **What is 'ECDSA key fingerprint'?**

Figerprint, specifically SSH host key fingerprint, is a fixed length key which is generated through the SSH host's public key. The fingerprint, since generated from public key, is not needed to be kept secret and can be shared.

You can generate the fingerprint with following  command,

```
.ssh % ssh-keygen -lf path/to/my/publicKey.pub
256 SHA256:thEkEyIcAnNotReVealBpDPWJRRGABCdefGhihNTA3+R0 akash (ED25519)
```

In recent versions of Open SSH the fingerprint is hashed with SHA-256 and encoded with Base64 by default. But different hashing algorithms can be used.

Here ED25519 is nothing but the digital signature algorithm used to generate public and private keys for the host. You may find RSA instead as it is the oldest one and majorly used.

But you may ask, why can't we directly check the public key, *what is the need of fingerprint?*, the answer is, fingerprints are concise which enables easy and quick identification of the host. 

Note that whenever the SSH is reconfigured on the host the public key will likely going to change and so as *fingerprint*. 


![fingerprint (1).jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1646497537098/4MhI6K-QR.jpg)

Consider a scenario where you are using a domain given to a load balancer and whenever you connect you may reach to different servers running behind the load balancer. Since your access point is same but the server which will going to connect can be different, your SSH client may not be able to recognize the host everytime as the fingerprints are different for each servers.


#### **What should we do?**

If you are 100% sure that the host you are trying to connect is correct, just input 'yes'. This will add the fingerprint of that server in your `~/.ssh/known_hosts` file. So, next time whenever you connect, it will not warn you but instead it will check the fingerprint from this file and continue, assuming you already 'know the host'. Since this will happen connecting very first time, better to check the fingerprint and then allow to connect. 

Afterwards, if you see this warning again for the same host, time to confirm whether SSH on host is reconfigured or anyhow the public key is changed for the host which end up mismatch of fingerprint. Even if you are communicating with private line between two servers, any other server tries to be an imposter, can be caught with this mechanism.

It is also possible to disable this warning by adding following parameter in SSH config (*~/.ssh/config*) file, 

```
Host *
  StrictHostKeyChecking no
```

However, this is **not** recommended and should be avoided whenever possible and can be used when *you really know what you are doing and what can happen doing so*.



