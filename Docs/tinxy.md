

## Tasmota config [source](ttps://forum.tinxy.in/t/flashing-custom-firmware-like-tasmota-or-esphome-and-then-restoring-back-to-original/32/24)

Template

```
{"NAME":"Tinxy 6 Node","GPIO":[224,0,0,0,225,226,0,0,320,227,228,229,0,0],"FLAG":0,"BASE":18}
```

And 2 rules, one for controlling the relays and one for manual switch operation

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


The 6 node I have on hand uses the GPIO pins 1 and 3 as a hardware serial bridge. 

as in the binary instruction, 1 being on and 0 being off. 
