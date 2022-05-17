

## Tasmota config 

Template

```
{"NAME":"Tinxy 6 Node","GPIO":[224,0,0,0,225,226,0,0,320,227,228,229,0,0],"FLAG":0,"BASE":18}
```

And 2 rules, one for controlling the relays and one for manual switch operation


### 4 Node 

```

Rule1 
ON System#Boot DO baudrate 9600 ENDON
ON Power1#State=1 DO serialsend2 #1100# ENDON
ON Power1#State=0 DO serialsend2 #1000# ENDON
ON Power2#State=1 DO serialsend2 #2100# ENDON
ON Power2#State=0 DO serialsend2 #2000# ENDON
ON Power3#State=1 DO serialsend2 #3100# ENDON
ON Power3#State=0 DO serialsend2 #3000# ENDON
ON Power4#State=1 DO serialsend2 #4100# ENDON
ON Power4#State=0 DO serialsend2 #4000# ENDON


rule2
ON System#Boot DO SerialSend2 1 ENDON
ON SerialReceived#Data=;10; DO Power1 0 ENDON
ON SerialReceived#Data=;11; DO Power1 1 ENDON
ON SerialReceived#Data=;20; DO Power2 0 ENDON
ON SerialReceived#Data=;21; DO Power2 1 ENDON
ON SerialReceived#Data=;30; DO Power3 0 ENDON
ON SerialReceived#Data=;31; DO Power3 1 ENDON
ON SerialReceived#Data=;40; DO Power4 0 ENDON
ON SerialReceived#Data=;41; DO Power4 1 ENDON

rule1 1
rule2 1
``` 


### 6 Node 

```
rule1 
on System#Boot do Baudrate 9600 endon
on Power1#State=1 do SerialSend2 #1100# endon
on Power1#State=0 do SerialSend2 #1000# endon
on Power2#State=1 do SerialSend2 #2100# endon
on Power2#State=0 do SerialSend2 #2000# endon
on Power3#State=1 do SerialSend2 #3100# endon
on Power3#State=0 do SerialSend2 #3000# endon
on Power4#State=1 do SerialSend2 #4100# endon
on Power4#State=0 do SerialSend2 #4000# endon
on Power5#State=1 do SerialSend2 #5100# endon
on Power5#State=0 do SerialSend2 #5000# endon
on Power6#State=1 do SerialSend2 #6100# endon
on Power6#State=0 do SerialSend2 #6000# endon

rule2
on System#Boot do SerialSend2 1 endon
on SerialReceived#Data=;10; do Power1 0 endon
on SerialReceived#Data=;11; do Power1 1 endon
on SerialReceived#Data=;20; do Power2 0 endon
on SerialReceived#Data=;21; do Power2 1 endon
on SerialReceived#Data=;30; do Power3 0 endon
on SerialReceived#Data=;31; do Power3 1 endon
on SerialReceived#Data=;40; do Power4 0 endon
on SerialReceived#Data=;41; do Power4 1 endon
on SerialReceived#Data=;50; do Power5 0 endon
on SerialReceived#Data=;51; do Power5 1 endon
on SerialReceived#Data=;60; do Power6 0 endon
on SerialReceived#Data=;61; do Power6 1 endon
```


The 6 node uses the GPIO pins 1 and 3 as a hardware serial bridge. 

[source](https://forum.tinxy.in/t/flashing-custom-firmware-like-tasmota-or-esphome-and-then-restoring-back-to-original/32/24)
